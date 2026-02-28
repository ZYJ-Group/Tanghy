# 3D-HGS: 3D Half-Gaussian Splatting｜组会口头汇报梳理

## 目录
- [A. 背景与问题定义](#a-背景与问题定义)
  - [A1. 论文解决什么问题？](#a1-论文解决什么问题)
  - [A2. 系统/几何/坐标系语境](#a2-系统几何坐标系语境)
- [B. 核心痛点——为什么传统方法不行](#b-核心痛点为什么传统方法不行)
  - [B1. 痛点 1：高斯核难以刻画不连续导致边界与纹理失真](#b1-痛点-1高斯核难以刻画不连续导致边界与纹理失真)
  - [B2. 痛点 2：直接把“半透明半高斯”当作完整高斯去 splat 会引入冗余计算](#b2-痛点-2直接把半透明半高斯当作完整高斯去-splat-会引入冗余计算)
- [C. 作者整体思路（总体框架）](#c-作者整体思路总体框架)
  - [C1. 端到端管线（Pipeline）](#c1-端到端管线pipeline)
- [D. 具体方法（模块化拆解）](#d-具体方法模块化拆解)
  - [D1. 模块 1：Preliminaries —— 3D-GS 的高斯核、投影与 alpha blending](#d1-模块-1preliminaries--3d-gs-的高斯核投影与-alpha-blending)
  - [D2. 模块 2：3D Half-Gaussian Kernel —— 用分割平面把一个高斯拆成两个半高斯并赋予双不透明度](#d2-模块-23d-half-gaussian-kernel--用分割平面把一个高斯拆成两个半高斯并赋予双不透明度)
  - [D3. 模块 3：3D Half-Gaussian Rasterization —— 半高斯对像素贡献的闭式形式与新的 blending 写法](#d3-模块-33d-half-gaussian-rasterization--半高斯对像素贡献的闭式形式与新的-blending-写法)
  - [D4. 模块 4：3D Half-Gaussian Splatting —— 为每个“半边”计算有效区域以避免冗余 tile](#d4-模块-43d-half-gaussian-splatting--为每个半边计算有效区域以避免冗余-tile)
- [E. 实验与结果（按论文逻辑组织）](#e-实验与结果按论文逻辑组织)
  - [E1. 实验组织总览](#e1-实验组织总览)
  - [E2. 全面基准：把 3D-GS 及其扩展替换成 Half-Gaussian 是否稳定提升质量](#e2-全面基准把-3d-gs-及其扩展替换成-half-gaussian-是否稳定提升质量)
  - [E3. 速度与显存：质量提升是否以速度/存储为代价](#e3-速度与显存质量提升是否以速度存储为代价)
  - [E4. “换核”对比：Half-Gaussian 相比 2D-GS 与 GES 的总体收益](#e4-换核对比half-gaussian-相比-2d-gs-与-ges-的总体收益)
  - [E5. 不连续拟合证据链：边缘列剖面与整图误差图说明了什么](#e5-不连续拟合证据链边缘列剖面与整图误差图说明了什么)
  - [E6. 质化证据：细节、纹理、光照与阴影区域的改进](#e6-质化证据细节纹理光照与阴影区域的改进)
- [F. 对比结论与复盘（必须有）](#f-对比结论与复盘必须有)
  - [F1. 作者声称的核心贡献点](#f1-作者声称的核心贡献点)
  - [F2. 基线痛点 → 本文解决点 → 证据闭环](#f2-基线痛点--本文解决点--证据闭环)
  - [F3. 局限性与未来工作](#f3-局限性与未来工作)

---

# A. 背景与问题定义
## A1. 论文解决什么问题？
- 任务定义：我们要讲清楚——作者关注 3D 场景重建后的新视角合成（NVS）与照片级渲染，核心目标是在保持 3D Gaussian Splatting（3D-GS）实时渲染优势的前提下，提升对形状与颜色不连续（边界、角点、纹理高频）的建模能力 (Abstract, Sec. 1)  
- 输入与输出：输入是由 SfM 得到的稀疏点云初始化，并在训练中通过渲染损失优化一组参数化核；输出是在给定相机视角下的渲染图像（并用 PSNR/SSIM/LPIPS 评估）(Sec. 3.1, Sec. 4.1)  
- 价值与动机：3D-GS 相比 NeRF 更快，但在不连续处容易出现模糊边缘与振铃等伪影；作者希望用“更适合不连续的核”作为可插拔替换，直接增强现有 3D-GS 体系而不牺牲速度 (Abstract, Sec. 1, Fig. 2)

## A2. 系统/几何/坐标系语境
- 高频符号（只列后文会反复用到的）(Sec. 3.1–3.3)  
  - 3D 点：$`x \in \mathbb{R}^3`$，高斯均值：$`\mu \in \mathbb{R}^3`$ (Eq. (1), Sec. 3.1)  
  - 协方差：$`\Sigma \in \mathbb{R}^{3\times 3}`$，相机系协方差的 2D 子矩阵：$`\hat{\Sigma} \in \mathbb{R}^{2\times 2}`$ (Eq. (3)–(5), Sec. 3.1)  
  - 不透明度：$`\alpha`$；Half-Gaussian 的双不透明度：$`\alpha_1, \alpha_2`$ (Sec. 3.2)  
  - 分割平面法向：$`n \in \mathbb{R}^3`$ (Eq. (7), Sec. 3.2)  
  - 像素坐标：$`\hat{x}=[x,y]^T`$，像素处的核响应用 $`\hat{G}`$ 或 $`\hat{HG}`$ 表示 (Eq. (4), Eq. (11), Sec. 3.1–3.3)  
- 图引用：Fig. 4 给出了训练/渲染流程、Half-Gaussian 对的参数化（共享均值与形状，区分双不透明度并引入分割平面法向），以及它在 ray space 到图像平面的映射关系 (Fig. 4)

---

# B. 核心痛点——为什么传统方法不行
## B1. 痛点 1：高斯核难以刻画不连续导致边界与纹理失真
- 现象：用完整高斯核去逼近具有尖锐边缘的不连续函数，会出现类似 Gibbs 现象的过冲/欠冲与非垂直过渡（边缘变“糊”）(Sec. 1, Fig. 2(a))  
- 根因：高斯核是强平滑的低通型重建核，在高频分量丰富的边界/纹理处表达效率低，难以用少量核准确表示尖锐变化 (Sec. 1, Fig. 2(c)–(d))  
- 证据落点：作者用 1D 方波拟合实验显示，Half-Gaussian 混合能用更少核得到更低误差，并在频域具有更高带宽，说明其更擅长捕获高频成分 (Fig. 2(b)–(d))

## B2. 痛点 2：直接把“半透明半高斯”当作完整高斯去 splat 会引入冗余计算
- 现象：Half-Gaussian 引入“双半边”，但大量样本中一侧几乎透明；如果仍按完整高斯那样对两侧统一 splat，会把许多“无贡献半边”也纳入 tile 处理，从而拖慢渲染 (Sec. 3.4, Fig. 5)  
- 根因：Half-Gaussian 的有效支持域是“被分割平面截断后的半空间”，其在屏幕空间对应的是半椭圆形的有效区域；若不显式裁剪有效区域，会产生大量冗余 tile 覆盖 (Sec. 3.4, Fig. 6)  
- 证据落点：Fig. 5 统计显示超过 75% 的 Half-Gaussian 核其两侧不透明度差异（归一化后）大于 0.5，支持“半边常常只负责局部有效区域”的说法；Fig. 6 进一步展示冗余 tile 与有效区域的关系 (Sec. 3.4, Fig. 5–6)

---

# C. 作者整体思路（总体框架）
## C1. 端到端管线（Pipeline）
- 我们要讲清楚作者的总体策略：  
  1) 保留 3D-GS 的训练/渲染大流程（初始化 → 投影 → 自适应密度控制 → rasterizer → 图像损失反传）不变；  
  2) 把“重建核”从完整 3D Gaussian 替换为 3D Half-Gaussian 对：共享均值、尺度、旋转、颜色，仅增加分割平面法向与第二个不透明度；  
  3) 在 rasterizer 中推导 Half-Gaussian 沿视线积分到 2D 的闭式形式，并据此修改前向/反向；  
  4) 在 splatting 阶段为每个“半边”计算其屏幕空间有效区域，避免对透明半边做无效 splat (Sec. 3, Fig. 4; Sec. 3.3–3.4)  
- 图引用：Fig. 4(a) 用一张图把训练与渲染的关键模块连起来，Fig. 4(b)–(c) 用“分割平面 + 双不透明度”的参数化解释 Half-Gaussian 如何映射到图像平面 (Fig. 4)

---

# D. 具体方法（模块化拆解）
## D1. 模块 1：Preliminaries —— 3D-GS 的高斯核、投影与 alpha blending (Sec. 3.1)
- 输入：SfM 初始化点云对应的一组 3D 高斯核参数（均值 $`\mu`$、协方差相关参数、颜色、单不透明度 $`\alpha`$）以及相机视角 (Sec. 3.1)  
- 输出：图像平面的 2D 高斯响应与最终像素颜色（通过 alpha blending 聚合）(Eq. (4)–(6), Sec. 3.1)  
- 关键技术点：  
  1) 用各向异性 3D 椭球高斯表示场景局部体渲染核 (Eq. (1), Sec. 3.1)  
  2) 协方差在世界系用 $`R,S`$ 参数化以确保正定，并通过相机变换与雅可比映射到相机系/图像系 (Eq. (2)–(3), Sec. 3.1)  
  3) 沿视线积分把 3D 高斯转为图像平面 2D 高斯，使 rasterization 可高效实现 (Eq. (4), Sec. 3.1)  
  4) 像素颜色由深度排序后的核集合做 alpha blending 得到 (Eq. (6), Sec. 3.1)  
- 关键公式：  

$$
\int_{\mathbb{R}} G_{\Sigma}(x-\mu)\, dz = \hat{G}_{\hat{\Sigma}}(\hat{x}-\hat{\mu}) .
$$
  - 含义：说明 3D 高斯沿视线方向积分后可得到图像平面的 2D 高斯，这是 3D-GS 高效 rasterization 的关键 (Eq. (4), Sec. 3.1)  
  - 符号：$`G_{\Sigma}`$ 为 3D 高斯核；$`x=[x,y,z]^T`$；$`\hat{x}=[x,y]^T`$；$`\hat{\Sigma}`$ 为投影后的 2D 协方差子矩阵 (Eq. (4), Sec. 3.1)  
- 关键公式：  

$$
C = \sum_{i \in \mathcal{N}} c_i \sigma_i \prod_{j=1}^{i-1} (1-\sigma_j), \quad \sigma_i = \alpha_i \hat{G}(\hat{x}-\hat{\mu}_i).
$$
  - 含义：把同一像素上按深度排序的一组 2D 核响应用前乘透射率的方式累积成最终颜色 (Eq. (6), Sec. 3.1)  
  - 符号：$`C`$ 为像素颜色；$`\mathcal{N}`$ 为该像素关联的排序核集合；$`c_i`$ 为颜色；$`\sigma_i`$ 为第 $`i`$ 个核在该像素处的不透明贡献 (Eq. (6), Sec. 3.1)  
- 流程步骤：  
  1) 由 SfM 点初始化高斯核并进入训练 (Sec. 3.1, Fig. 4(a))  
  2) 把 3D 核投影并在图像平面形成 2D 核响应 (Eq. (4), Sec. 3.1)  
  3) 在每个像素做排序与 alpha blending 得到渲染图 (Eq. (6), Sec. 3.1)

## D2. 模块 2：3D Half-Gaussian Kernel —— 用分割平面把一个高斯拆成两个半高斯并赋予双不透明度 (Sec. 3.2)
- 输入：原 3D 高斯的几何与颜色参数（均值、协方差、颜色）外加分割平面法向 $`n`$ 与双不透明度 $`\alpha_1,\alpha_2`$ (Sec. 3.2, Fig. 4(b))  
- 输出：一个“成对表示”的 Half-Gaussian 重建核（共享形状，仅半空间响应不同），并保留在 $`\alpha_1=\alpha_2`$ 时退化回原 3D-GS 核 (Sec. 3.2)  
- 关键技术点：  
  1) 用过中心的分割平面把高斯分成两个半空间响应，核心是一个指示条件 $`n^T(x-\mu)\ge 0`$ (Eq. (7), Sec. 3.2)  
  2) 两半共享均值、旋转、尺度、颜色，只区分双不透明度；因此参数增量很小 (Sec. 3.2)  
  3) 作者指出实现上可复用 3D-GS kernel 中未使用的 normal 字段存储 $`n`$，实际额外内存仅增加一个不透明度参数 (Sec. 3.2, Sec. 4.1)  
  4) 直觉解释：Half-Gaussian 在频域具有更高带宽，因而更能表达不连续处的高频成分 (Sec. 1, Fig. 2(d))  
- 关键公式：  

$$
HG_{\Sigma}(x-\mu)=
\begin{cases}
\exp\!\left(-\tfrac{1}{2}(x-\mu)^T \Sigma^{-1}(x-\mu)\right), & n^T(x-\mu)\ge 0, \\
0, & n^T(x-\mu)<0.
\end{cases}
$$
  - 含义：定义“半高斯”核为在一个半空间保留原高斯形状、在另一半空间置零，从而把核的支持域变成可表达边界的不对称形状 (Eq. (7), Sec. 3.2)  
  - 符号：$`n`$ 为分割平面法向；$`x`$ 为 3D 点；$`\mu`$ 为核中心；$`\Sigma`$ 为协方差 (Eq. (7), Sec. 3.2)  
- 关键公式：  

$$
\int_{n^T(x-\mu)\ge 0} HG_{\Sigma}(x-\mu)\, dz
= \tfrac{1}{2}\, I(x,y)\, \hat{G}_{\hat{\Sigma}}(\hat{x}-\hat{\mu}) .
$$
  - 含义：Half-Gaussian 沿视线积分后仍可写成“2D 高斯乘以一个尺度因子”，尺度因子刻画分割平面对该像素的截断效应 (Eq. (8), Sec. 3.2)  
  - 符号：$`I(x,y)`$ 为与分割平面相关的尺度因子；$`\hat{G}_{\hat{\Sigma}}`$ 为投影到图像平面的 2D 高斯 (Eq. (8), Sec. 3.2)  

## D3. 模块 3：3D Half-Gaussian Rasterization —— 半高斯对像素贡献的闭式形式与新的 blending 写法 (Sec. 3.3)
- 输入：Half-Gaussian 对的共享几何/颜色参数（均值、协方差、颜色）与双不透明度 $`\alpha_1,\alpha_2`$，以及分割法向 $`n`$ (Sec. 3.3, Fig. 4(b)–(c))  
- 输出：用于 rasterizer 的像素贡献函数 $`\hat{HG}(\hat{x}-\hat{\mu})`$，并在像素级用新的 alpha blending 公式累积颜色 (Eq. (10)–(11), Sec. 3.3)  
- 关键技术点：  
  1) 参数共享：一对 Half-Gaussian 共享均值、旋转、尺度、颜色，仅学习分割平面方向与两侧不透明度，提高参数效率 (Sec. 3.3)  
  2) 渲染表达：把“两半积分结果”合并成一个等效的 2D 响应 $`\hat{HG}`$，其形式仍是 2D 高斯乘以可学习的系数 (Eq. (11), Sec. 3.3)  
  3) rasterizer 前向与反向在 vanilla 3D-GS 基础上按 $`\hat{HG}`$ 修改，保持整体计算框架不变 (Sec. 4.1)  
- 关键公式：  
$$
C = \sum_{i \in \mathcal{N}} c_i\, \hat{HG}_i(\hat{x}-\hat{\mu}_i)\, \prod_{j=1}^{i-1}\bigl(1-\hat{HG}_j(\hat{x}-\hat{\mu}_j)\bigr).
$$
  - 含义：把原 3D-GS 的 $`\sigma_i`$ 替换成 Half-Gaussian 的像素响应 $`\hat{HG}`$，其余排序与透射率累积结构保持一致 (Eq. (10), Sec. 3.3)  
  - 符号：$`\mathcal{N}`$ 为排序核集合；$`c_i`$ 为颜色；$`\hat{HG}_i`$ 为第 $`i`$ 个 Half-Gaussian 对在像素处的等效响应 (Eq. (10), Sec. 3.3)  
- 关键公式：  

$$
\hat{HG}(\hat{x}-\hat{\mu})
= \tfrac{1}{2}\Bigl(2\alpha_2 + (\alpha_1-\alpha_2)\, I(x,y)\Bigr)\, \hat{G}_{\hat{\Sigma}}(\hat{x}-\hat{\mu}) .
$$
  - 含义：给出“一对 Half-Gaussian 积分到图像平面后”的闭式贡献：仍是 2D 高斯形状，但幅度由双不透明度与尺度因子 $`I(x,y)`$ 调制，从而能在不连续处实现更细粒度控制 (Eq. (11), Sec. 3.3)  
  - 符号：$`\alpha_1,\alpha_2`$ 为两侧不透明度；$`I(x,y)`$ 为由分割平面决定的尺度因子；$`\hat{G}_{\hat{\Sigma}}`$ 为 2D 高斯 (Eq. (11), Sec. 3.3)  
- 流程步骤：  
  1) 对每个核对计算投影到图像平面的 $`\hat{G}_{\hat{\Sigma}}`$ (Sec. 3.1, Eq. (4))  
  2) 计算尺度因子 $`I(x,y)`$ 并代入得到 $`\hat{HG}`$ (Sec. 3.2–3.3, Eq. (8)–(11))  
  3) 对每个像素按深度排序并用 Eq. (10) 累积颜色 (Sec. 3.3, Eq. (10))

## D4. 模块 4：3D Half-Gaussian Splatting —— 为每个“半边”计算有效区域以避免冗余 tile (Sec. 3.4)
- 输入：Half-Gaussian 对投影到屏幕空间后的几何形状，以及分割平面在图像上的投影（“splitting surface” 投影为一条椭圆边界）(Sec. 3.4, Fig. 6)  
- 输出：每个半边在屏幕上的最小包围矩形（bounding rectangle）与最终的有效 splat 区域，用于减少 tile 覆盖与无效渲染 (Sec. 3.4, Fig. 6)  
- 关键技术点：  
  1) 动机：大量核的一侧几乎透明，必须避免把透明半边也当作有效核去覆盖 tile (Sec. 3.4, Fig. 5)  
  2) 内界：先把椭球分割面投影到图像平面，得到相对投影中心的“内矩形” (Sec. 3.4, Fig. 6 左)  
  3) 外界：参考 FlashGS 的思路计算分割椭圆切线边缘相对中心的宽高，得到外边界 (Sec. 3.4, Fig. 6 左)  
  4) 最终有效区域：用能同时覆盖“投影分割椭圆 + 切线边缘”的最小包围矩形作为处理范围，并区分“单侧透明”与“双侧贡献”两种情况 (Sec. 3.4, Fig. 6 中/右)  
- 流程步骤：  
  1) 投影分割椭球面到图像平面，得到分割椭圆 (Sec. 3.4, Fig. 6)  
  2) 计算切线边缘确定外界，构造最小包围矩形 (Sec. 3.4)  
  3) 若一侧透明，仅 splat 不透明侧；若两侧均贡献，联合分割椭圆与外界确定有效区域 (Sec. 3.4, Fig. 6)

---

# E. 实验与结果（按论文逻辑组织）
## E1. 实验组织总览
- 我们要讲清楚作者的验证链路：  
  1) 先给出动机证据（方波拟合、频域带宽）说明 Half-Gaussian 更适合不连续 (Sec. 1, Fig. 2)  
  2) 再做“可插拔替换”主实验：把 3D-GS 及其三个扩展方法的核替换为 Half-Gaussian，观察跨数据集的质量提升是否一致 (Sec. 4.1–4.2, Table 1, Fig. 3)  
  3) 同时汇报速度与存储，验证不牺牲实时性 (Sec. 4.2, Table 2, Fig. 3)  
  4) 增加两条证据链：对比其他“换核”方法（2D-GS、GES），以及用误差剖面/误差热图与质化图像解释提升来自不连续处的拟合改进 (Sec. 4.2, Table 3, Fig. 7–9)

## E2. 全面基准：把 3D-GS 及其扩展替换成 Half-Gaussian 是否稳定提升质量 (Sec. 4.1–4.2)
- 要回答的问题：Half-Gaussian 作为 plug-and-play kernel，是否能在不同 splatting 架构上带来一致的质量收益 (Abstract, Sec. 4.2)  
- 设置：11 个场景，来自 Mip-NeRF360（7）、Tanks&Temples（2）、Deep Blending（2）；指标用 PSNR、SSIM、LPIPS；报告各数据集平均，并在附录给出逐场景结果 (Sec. 4.1)  
- 对比：以 vanilla 3D-GS、Scaffold-GS、Mip-Splatting、GS-MCMC 为四个基线，把重建核替换为 Half-Gaussian，得到 3D-HGS、Scaffold-HGS、Mip-Splatting-HGS、HGS-MCMC；并与 Mip-NeRF、2D-GS、FreGS、GES 等方法对比 (Sec. 4.1)  
- 结果与结论：Table 1 显示在三套数据集上，Half-Gaussian 版本均优于对应基线；例如在 Mip-NeRF360 上 3D-HGS 相比 3D-GS 的 PSNR 提升 0.78，在 Tanks&Temples 上提升 0.85，在 Deep Blending 上提升 0.35；HGS-MCMC 在多个数据集上达到新的最优 PSNR (Sec. 4.2, Table 1)

## E3. 速度与显存：质量提升是否以速度/存储为代价 (Sec. 4.2)
- 要回答的问题：Half-Gaussian 引入双半边与额外参数，是否会显著降低 FPS 或增加显存/模型存储 (Abstract, Sec. 4.2)  
- 设置：报告 FPS 与存储（Mem），并给出 PSNR 与 FPS 的散点关系 (Fig. 3, Table 2)  
- 结果与结论：  
  - Fig. 3 显示在多种 SOTA splatting 方法上，把核替换为 Half-Gaussian 能显著提升 PSNR，同时 FPS 保持相近甚至更好 (Fig. 3)  
  - Table 2 显示多数设置下 FPS 变化很小，且 3D-HGS 甚至在多个数据集上比 3D-GS 更快；存储变化也不显著 (Table 2)  
  - 作者解释参数开销很小：实现上复用 3D-GS 中未使用的 normal 字段存储分割法向，额外只增加一个不透明度参数；同时通过“半边有效区域” splatting 避免冗余 tile (Sec. 4.1, Sec. 3.4, Fig. 6)

## E4. “换核”对比：Half-Gaussian 相比 2D-GS 与 GES 的总体收益 (Sec. 4.2)
- 要回答的问题：与其他核修改思路（2D-GS 的 2D 高斯、GES 的 generalized exponential kernel）相比，Half-Gaussian 是否更稳定地提升各场景 PSNR (Sec. 4.1–4.2)  
- 设置：在相同训练迭代与损失下，对比不同重建核在各场景的 PSNR，并给出数据集平均与总体平均 (Sec. 4.1, Table 3)  
- 结果与结论：Table 3 显示 3D Half-Gaussian 在所有场景上持续改进并取得最佳总体平均；而其他核在部分场景有提升但在另一些场景会退化，整体一致性不如 Half-Gaussian (Sec. 4.2, Table 3)

## E5. 不连续拟合证据链：边缘列剖面与整图误差图说明了什么 (Sec. 4.2)
- 要回答的问题：质量提升是否主要来自对“平滑区域 + 尖锐过渡”混合场景的拟合改善 (Sec. 4.2)  
- 设置：在 Bonsai 场景上取包含平滑与尖锐过渡的一列像素，比较 3D-GS 与 3D-HGS 的灰度拟合曲线，并给出整图误差热图 (Sec. 4.2, Fig. 7)  
- 结果与结论：Fig. 7 显示 3D-HGS 在包含尖锐过渡的列剖面处更贴近真值，误差峰值更小；整图误差热图也表明高误差区域在边界附近显著减少，支撑“Half-Gaussian 更擅长不连续处拟合”的核心论点 (Sec. 4.2, Fig. 7)

## E6. 质化证据：细节、纹理、光照与阴影区域的改进 (Sec. 4.2)
- 要回答的问题：从视觉上，Half-Gaussian 是否带来更清晰的细节与纹理、更稳定的光照与阴影表现 (Sec. 4.2)  
- 结果与结论：  
  - Fig. 8 的多场景对比显示 3D-HGS 在细节（结构边缘）、高频纹理、复杂光照与阴影区域更接近 GT，并在帧 PSNR 与平均 PSNR 上体现优势 (Sec. 4.2, Fig. 8)  
  - Fig. 9 进一步对比深度图与由深度估计的法线图，作者强调 Half-Gaussian 版本能恢复更细的结构细节与表面纹理 (Sec. 4.2, Fig. 9)

---

# F. 对比结论与复盘（必须有）
## F1. 作者声称的核心贡献点
- 贡献 1：提出 3D Half-Gaussian（3D-HGS）作为新的重建核，是一种可插拔替换方案，用于提升 3D-GS 在不连续处的建模能力 (Abstract, Sec. 1)  
- 贡献 2：在 Mip-NeRF360、Tanks&Temples、Deep Blending 上实现新的渲染质量最优水平，同时不牺牲渲染速度 (Abstract, Sec. 4.2, Table 1, Fig. 3)  
- 贡献 3：展示通用性：把 Half-Gaussian 核应用到多种 3D-GS 扩展（Scaffold-GS、Mip-Splatting、GS-MCMC）上，均带来稳定提升 (Sec. 4.1–4.2, Table 1)

## F2. 基线痛点 → 本文解决点 → 证据闭环
- 闭环 1（不连续建模失败）：  
  - 痛点：完整高斯核对尖锐边界/高频纹理表达效率低，导致过冲/欠冲与模糊边缘 (Sec. 1, Fig. 2(a))  
  - 解决点：用分割平面把高斯变成 Half-Gaussian，对两侧赋予不同不透明度，让核在不连续处具备更强的高频刻画能力 (Sec. 3.2, Fig. 4(b), Eq. (7))  
  - 证据：方波拟合与频域带宽对比说明 Half-Gaussian 更擅长捕获高频；Bonsai 的列剖面与误差热图显示边界处误差显著降低 (Fig. 2, Fig. 7, Sec. 4.2)  
- 闭环 2（插件化增强是否成立）：  
  - 痛点：很多改进方法依赖结构性变更，难在不同 splatting 框架上通用 (Sec. 2.2)  
  - 解决点：Half-Gaussian 保留 3D-GS 的整体流程，仅替换重建核与对应 rasterizer 计算，面向现有方法可直接替换 (Sec. 3, Sec. 4.1)  
  - 证据：在 3D-GS、Scaffold-GS、Mip-Splatting、GS-MCMC 四种基线上，Half-Gaussian 版本的 PSNR 均稳定提升，并多处达到新的最优 (Table 1, Sec. 4.2)  
- 闭环 3（速度与存储是否保住）：  
  - 痛点：增强核的表达力往往会引入额外计算或显存开销 (Sec. 1)  
  - 解决点：参数增量很小（额外一个不透明度；法向复用已有字段），并为每个半边计算有效区域以减少冗余 tile (Sec. 3.2, Sec. 3.4, Fig. 6)  
  - 证据：PSNR-FPS 曲线显示在多方法上 PSNR 提升同时 FPS 基本不变；速度与存储表显示开销不显著 (Fig. 3, Table 2)

## F3. 局限性与未来工作
- 文中主要强调“在不增加推理时间的情况下提升质量，并可无结构改动融入多数 Gaussian-splatting 架构”；结论部分未展开专门的局限性列表或未来工作方向 (Sec. 5)
