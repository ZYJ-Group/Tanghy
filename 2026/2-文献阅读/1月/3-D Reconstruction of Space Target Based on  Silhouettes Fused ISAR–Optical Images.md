# 3-D Reconstruction of Space Target Based on Silhouettes Fused ISAR–Optical Images（TGRS 2024）

> Bo Long, Pengling Tang, Feng Wang, Ya-Qiu Jin, “3-D Reconstruction of Space Target Based on Silhouettes Fused ISAR–Optical Images,” *IEEE TGRS*, 2024.（Abstract, Sec. I）

---

# A. 背景与问题定义
## A1. 论文解决什么问题？
- 任务定义：本文研究在 **ISAR–光学同址（co-location）同步观测**条件下，利用两类 2-D 投影图像（ISAR range–Doppler 与 optical 成像平面）进行 **基于轮廓（silhouette）的 3-D 体素重建**，并同时实现 **旋转/自旋目标的动态参数估计**（attitude 与有效旋转向量相关量）。
- 场景与假设：目标为在轨飞行空间目标；光学与 ISAR 可在同站同步获取，且在远距离条件下可近似为正交投影；目标可能为三轴稳定或存在自旋（spinning）。
- 重要性：SSA 需要空间目标 3-D 信息；仅靠 ISAR 难以在自旋场景确定动态姿态与投影关系，光学图像又常因过曝/过暗与扰动导致纹理不足，故需要统一、稳健的轮廓类信息并进行跨模态融合。

## A2. 系统/几何/坐标系语境
- 同址几何：ISAR 与 optical 传感器位于同一站点；两者成像平面近似正交（co-location + synchronized observation 形成两正交投影平面）。
- 坐标系：建立雷达坐标系（东/北/上）与目标轨道坐标系 $`O'XYZ`$；LOS 向量从雷达系变换到轨道系，以角 $`\theta,\phi`$ 参数化。
- 关键测量量/符号：ISAR 的距离向投影向量 $`\mathbf{k}_{\mathrm{radar},r}`$ 与多普勒向（方位）投影向量 $`\mathbf{k}_{\mathrm{radar},d}`$；光学投影向量 $`\mathbf{k}_{\mathrm{optical},u},\mathbf{k}_{\mathrm{optical},v}`$；有效旋转向量 $`\boldsymbol{\omega}_{\mathrm{eff}}`$；目标结构线特征（太阳翼长/短边）$`\mathbf{s}_l,\mathbf{s}_s`$。
<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/eea038f1-925c-4ecb-97eb-5455e4a89dba" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/e8e3c76b-8c77-4bd9-b48e-cabd01905287" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/3893619f-ad8d-46be-8015-7c826486fcd3" width="360" /></td>
  </tr>
</table>

图1 .共定位ISAR -光学观测几何。图2 .与ISAR成像相关的矢量定义。图3 . ISAR与光学成像面的关系。

---

# B. 核心痛点——为什么传统方法不行
## B1. 痛点 1：仅靠 ISAR 难以确定自旋目标的动态姿态与投影向量
- 现象：自旋目标的 3-D 重建需要正确投影关系；仅用 ISAR 难以确定动态姿态/有效旋转，从而难以确定 ISAR 方位投影向量与尺度。
- 根因：ISAR 方位投影由 $`\boldsymbol{\omega}_{\mathrm{eff}}`$ 与 LOS 共同决定；自旋使 $`\boldsymbol{\omega}_{\mathrm{eff}}`$ 不再等同轨道导致的 $`\boldsymbol{\omega}_{\mathrm{LOS}}`$，且仅 $`\boldsymbol{\omega}_{\mathrm{synthesis}}`$ 在 LOS 垂直分量起作用。
- 文中证据：Configuration I（仅用 ISAR 且仅用 LOS 推断）重建失败，体素 IOU 很低（平均 0.1469）。

## B2. 痛点 2：光学图像纹理不足，难以直接用 SFM/立体等依赖特征匹配的方法
- 现象：光学图像存在过曝/过暗与大气扰动，导致细节特征不足，难以稳定做特征提取与匹配。
- 根因：空间目标光学成像条件非理想（太阳辐照强、目标指向/姿态、扰动等），使传统特征点/纹理驱动 3-D 方法不稳。
- 文中证据：Fig. 4 给出实测 ISAR/光学图像示例，体现光学细节不足、ISAR 散射离散。

## B3. 痛点 3：散射点/散射中心路线在空间目标场景易受各向异性与遮挡影响
- 现象：基于散射点提取与关联（如 OFM）在散射各向异性与遮挡下难以稳健完成。
- 根因：散射中心提取与跨视角关联困难，且系统/几何复杂度高；部分 3-D ISAR 方法还要求三轴稳定或高对准精度（如 InISAR）。
- 文中证据：本文明确提出“Instead of adopting a scattering point-based method”并转向轮廓/结构级表示以实现结构级体素重建。

<img alt="image" src="https://github.com/user-attachments/assets/1cd33964-0f82-4980-8d45-5bf2ce5f566f" width="360" />

图4 .测量了空间目标的ISAR和光学图像。( a )微波遥感卫星的ISAR像；( b )微波遥感卫星的光学像，由欧空局的Pleiades卫星拍摄。( c )天宫岛- 1 . ( d )天宫一号的光学图像，由业余天文学家拍摄。( a )和( c )由FHR宽带雷达获得。

---

# C. 作者整体思路
## C1. 总体策略/链路（Pipeline）
- 输入：同址同步的 ISAR–optical 图像对序列（多帧），以及光学已知的投影信息/标定信息与 LOS 信息。
- 关键步骤：
  1) 结构分割：用语义分割网络得到 ISAR 结构级 mask（body/panel/overlap/background），并对太阳翼区域做几何先验（平行四边形）拟合以提取投影长度特征。
  2) 动态参数估计：基于两非共线线特征（太阳翼长/短边）在 ISAR 与光学两平面上的投影长度，最小二乘求解 3-D 方向向量 $`\mathbf{s}_l,\mathbf{s}_s`$，并进一步解 ISAR 方位投影向量 $`\mathbf{k}_{\mathrm{radar},d}`$ 与 $`\|\boldsymbol{\omega}_{\mathrm{eff}}\|`$。
  3) 投影统一与校准：把不同帧姿态对齐到参考帧；利用 $`\|\boldsymbol{\omega}_{\mathrm{eff}}\|`$ 校准 ISAR 方位向分辨率/尺度，使 ISAR 与光学在统一“等效相机投影矩阵”下投影一致。
  4) 体素重建：对候选体素网格做多帧投影一致性累积与阈值化，得到结构级 3-D 体素集合并输出结构类型。
- 输出：结构级 3-D 体素重建（body/panel/overlap）与自旋目标动态参数估计结果（$`\mathbf{s}_l,\mathbf{s}_s,\mathbf{k}_{\mathrm{radar},d},\|\boldsymbol{\omega}_{\mathrm{eff}}\|`$ 等）。
- Fig. 11：给出整体算法流程图，将“分割+特征→参数估计→投影/尺度校准→体素累积重建”串联为完整论证链。
<img alt="image" src="https://github.com/user-attachments/assets/b6684fc6-3b42-4fba-8918-df89298d059d" width="360" />

图11 .总体算法流程图。


# D. 具体方法（精简版：仅保留关键公式）

## D1. Joint ISAR–Optical Co-location Geometry（同址成像几何）—统一两模态投影语境
- 输入：LOS 序列、目标轨道坐标系定义、雷达波长 $`\lambda`$、CPI 等。
- 输出：ISAR 两轴投影向量、光学投影向量/矩阵表达，以及正交投影近似成立条件。
- 关键点：把 ISAR 与 optical 都写成“3-D 点到 2-D 坐标”的投影形式，后续可统一做 silhouette-based 重建。
- 流程：定义坐标系与 LOS → 得到 ISAR 投影向量与 optical 投影基底 → 为后续统一 silhouette 投影做准备。

---

## D2. Dynamic Parameter Estimation（动态参数估计）—由两模态投影长度恢复 ISAR 方位投影与有效旋转
- 输入：太阳翼长/短边投影长度特征（ISAR 与 optical），以及已知 $`\mathbf{k}_{\mathrm{optical},u},\mathbf{k}_{\mathrm{optical},v},\mathbf{k}_{\mathrm{radar},r}`$。
- 输出：$`\mathbf{k}_{\mathrm{radar},d}`$ 与 $`\|\boldsymbol{\omega}_{\mathrm{eff}}\|`$ 等动态量。
- 关键点：先用三条投影约束恢复 3-D 边向量，再用光学基底参数化 ISAR 方位向，从而把未知量降维。

$$
\mathbf{A}\mathbf{s}=\mathbf{b},\quad
\mathbf{A}=
\begin{bmatrix}
\mathbf{k}_{\mathrm{optical},u}\\
\mathbf{k}_{\mathrm{optical},v}\\
\mathbf{k}_{\mathrm{radar},r}
\end{bmatrix},\quad
\mathbf{b}=
\begin{bmatrix}
\hat{\Delta u}\\
\hat{\Delta v}\\
\hat{\Delta r}
\end{bmatrix}
$$

含义：用“光学两维 + ISAR 距离向”三条投影约束恢复某条边的 3-D 向量 $`\mathbf{s}`$（长边/短边分别估计）。  
（Eq. (10), Sec. III-A）

$$
\mathbf{k}_{\mathrm{radar},d}
=\cos\alpha_{\mathrm{opt2d}}\ \mathbf{k}_{\mathrm{optical},v}
+\sin\alpha_{\mathrm{opt2d}}\ \mathbf{k}_{\mathrm{optical},u}
$$

含义：将 ISAR 方位向投影在光学正交基底上参数化，未知量由 3-D 向量降到单角度 $`\alpha_{\mathrm{opt2d}}`$。  
（Eq. (13), Sec. III-A）

$$
\|\boldsymbol{\omega}_{\mathrm{eff}}\|
=\frac{a_l\hat{\Delta d}_l+a_s\hat{\Delta d}_s}{a_l^2+a_s^2},\qquad
a_l=\mathbf{k}_{\mathrm{radar},d}\cdot \mathbf{s}_l,\ \ a_s=\mathbf{k}_{\mathrm{radar},d}\cdot \mathbf{s}_s
$$

含义：在得到 $`\mathbf{k}_{\mathrm{radar},d}`$ 与两条边 3-D 向量后，估计有效旋转角速度幅值。  
（Eq. (20), Sec. III-A）

- 流程：由投影长度解 $`\mathbf{s}_l,\mathbf{s}_s`$ → 由光学基底求 $`\mathbf{k}_{\mathrm{radar},d}`$ → 得到 $`\|\boldsymbol{\omega}_{\mathrm{eff}}\|`$。

---

## D3. Structure Segmentation & Feature Extraction（结构分割与特征提取）—获得 silhouette 与投影长度特征
- 输入：ISAR 图像。
- 输出：结构级分割结果（silhouette/结构标签）与太阳翼投影长度特征（供 D2 使用）。
- 关键点：通过语义分割得到稳定轮廓，再做几何拟合提取长/短边投影长度。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/baf763f7-7ed9-4a07-80a6-3e92f9a6ef80" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/befd2465-0e36-4960-a165-4a1c919266f5" width="360" /></td>
  </tr>
</table>
图7. Deeplabv3 +框架。图8. 基于几何先验知识的太阳能电池板平行四边形拟合。

---

## D4. Projection Alignment & ISAR Azimuth Calibration（投影对齐与方位尺度校准）—统一跨帧几何与尺度
- 输入：各帧估计的太阳翼基向量与投影向量。
- 输出：对齐后的投影向量与尺度一致的 ISAR 方位向。
- 关键点：跨帧对齐保证投影一致；方位尺度校准保证 ISAR 像素尺度可比。

<img src="https://github.com/user-attachments/assets/d111f97b-76ab-491c-9981-2f2a0fb52e88" width="360" />

图9. ISAR图像方位向定标(实际方位分辨率大于参考分辨率的情况)。

---

## D5. Uniform Silhouette-based Voxel Reconstruction（统一 silhouette 的体素重建）—两模态融合的 SFS
- 输入：多帧 optical/ISAR silhouette 与对应投影关系。
- 输出：体素占据结果与结构类别。
- 关键点：把 ISAR 写成等效相机投影，与 optical 一起对体素做多帧一致性“投票/累积”。

<img src="https://github.com/user-attachments/assets/de1251fe-6a88-4ed2-b3b0-e65c7631b10a" width="360" />

图10 .基于结构轮廓的三维重建。

$$
\begin{bmatrix}
X_V\\ Y_V
\end{bmatrix}
=\mathbf{P}\mathbf{V}
$$

含义：候选体素投影到像素平面，用 silhouette 一致性判定该体素是否被支持。  
（Eq. (34), Sec. IV-B）

$$
E(x,y,z)=\sum_{i=1}^{K} e_i(x,y,z),\qquad
V(x,y,z)=\{(x,y,z)\mid E(x,y,z)>\mathrm{thr}\}
$$

含义：多帧累积计数并阈值筛选得到最终体素集合。  
（Eq. (37)–(38), Sec. IV-B）

# E. 实验与结果

## E1. 证明结构分割网络可获得高质量结构级轮廓
- 目的：验证 ISAR 结构级语义分割的准确性与相对优势。
- 设置：训练数据为全视角大规模仿真 ISAR 数据；测试集为自旋目标轨道数据；指标为各类别 IOU。
- 对比：FCN、U-Net、PSPNet、Segmenter、Segformer 与 CFAR 阈值法。
- 结论：
  - Deeplabv3+ 在 Table V 中总体最好，尤其 solar panel IOU 超过 0.87；前景/背景平均 IOU 超过 0.90。
  - 相比 CFAR 的前景阈值分割（IOU 约 0.7635），NN 显著更好，且轮廓更闭合、更完整。
  - 论文指出轮廓不准将直接导致 3-D 重建不准。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/b24c5b2b-b059-462b-b9d5-9b64d036f625" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/a332d488-54e6-4f1b-843c-8f434b0470ad" width="360" /></td>
  </tr>
</table>

表IV三类空间目标数据集中的图像数量。 表V结构分割Iou比较。


<img src="https://github.com/user-attachments/assets/8e5d2322-9a05-4a44-b5d4-9ba7f110b5d1" width="360" />

图15。ISAR结构分割结果对比。第一列是Aura，第二列是微波遥感卫星，第三列是Tiangong - 1。每一行对应第一列左上方标注的不同方法。

## E2. 证明几何先验+拟合可稳定提取太阳翼投影长度特征并提升动态估计精度
- 目的：验证投影长度特征提取的误差分布，以及基于该特征的动态参数估计精度。
- 设置：先用分割得到太阳翼 mask，再拟合平行四边形提取长/短边投影长度；定义相对误差 ratio 统计直方图；动态参数误差用长度误差与角误差统计。
- 对比：本文方法 vs PCA 主成分法 vs Radon 变换方向法。
- 结论：
  - Fig. 16 显示即使预测 mask 不完整，拟合的平行四边形仍与 GT 大体一致，体现对“局部缺失”的鲁棒性。
  - Fig. 17 显示本文方法的相对误差集中在 0 附近，长/短边误差通常在 0.05–0.1；PCA 与 Radon 对短边误差明显更大且常“基本不正确”。
  - Table VII 给出动态参数误差统计：本文方法长边/短边角误差均值约 $`0.418^\circ/1.092^\circ`$，$`\mathbf{k}_{\mathrm{radar},d}`$ 角误差均值约 $`1.461^\circ`$，累积角误差均值约 $`0.250^\circ`$；而 PCA/Radon 在短边与累积角上误差显著更大。
  - 论文同时说明存在少量“坏例”（特定角度分割失败），实验中通过人工剔除明显错误帧（30→23 帧）。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/eb3971fa-67f5-49f1-98eb-04b90e842680" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/636ebe30-677b-4aa0-b605-1210508697b2" width="360" /></td>
  </tr>
</table>
图16 .预测面板掩模及其拟合平行四边形。第一列是Aura，第二列是微波遥感卫星，第三列是Tiangong - 1。不同的行代表不同的情况。 
图17 . 3种不同方法得到的太阳能电池板投影长度特征的相对误差(即,比率)。( a )和( b )长边/短边误差统计直方图，分别由所提出的方法获得。( c )和( d )由PCA得到，( e )和( f )由Radon变换得到。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/acb5c38c-a0bf-4040-b73b-ffb4e5d9b8db" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/d7915fd8-baa1-4b8d-bc43-fd41dce9db84" width="360" /></td>
  </tr>
</table>
表6投影长度特征及动态参数估计结果。表7动态参数的估计误差统计。

## E3. 证明 joint ISAR–optical 在三轴稳定条件下优于仅 ISAR（对应：Sec. V-D, Table VIII, Fig. 18–19）
- 目的：验证在三轴稳定目标场景下，联合观测对 3-D 结构信息的增益。
- 设置：每目标使用 10 个 joint 帧（共 20 张图），分别做 only ISAR、only optical、ISAR–optical；指标为 voxel IOU。
- 对比：only ISAR vs only optical vs joint。
- 结论：
  - Table VIII 显示 only ISAR 的 voxel IOU 极低（如 Aura 0.0376、ENVISAT 0.0353、Tiangong-1 0.1109），only optical 与 joint 明显更高（均 > 0.6）。
  - 文中解释：三轴稳定单次过站时 LOS 序列近似位于目标坐标系的扇形平面，ISAR 图像主要表现为绕中心旋转，难提供足够 3-D 几何信息，导致重建呈“柱状”。
  - joint 情况可获得更丰富几何信息，但三轴稳定条件下 3-D 信息主要由 optical 贡献。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/d589d05c-ff04-42df-8c03-2aa306293d9c" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/7ece5590-8abb-46b9-b17a-f105b072f2ca" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/1673b495-255e-4cf2-a410-ada720a71a19" width="360" /></td>
  </tr>
</table>
图18 .目标轨道坐标系下视轴矢量序列的可视化。( a )、( b )分别为三轴稳定条件和自旋条件的Aura ' s LOS序列。( c )、( d )分别为三轴稳定工况和自旋工况的微波遥感卫星LOS序列。( e )和( f )分别是三轴稳定条件和自旋条件下Tiangong - 1的LOS序列。 
图19 .三轴稳定目标重建结果。第一列是Aura，第二列是微波遥感卫星，第三列是Tiangong - 1。( a ) - ( c )仅Isar图像。( d ) - ( f ) ISAR -光学图像对。表8三轴稳定目标重构Iou。

## E4. 证明自旋场景下“投影向量估计 + 方位尺度校准 + 高质量 silhouette”是 joint 重建成功的必要条件
- 目的：分离验证投影向量估计、ISAR 方位校准与 silhouette 质量对重建的影响。
- 设置：自旋目标下设计 8 种配置（是否使用 optical/ISAR、silhouette 类型、是否做投影向量估计、是否做方位校准）；每配置 10 个 joint 帧；阈值 thr 取候选体素最大累积的 95%。
- 对比：Configuration I–VIII。
- 结论：
  - Configuration IV（joint 但不做投影向量估计与方位校准）失败，说明错误投影关系会“显著破坏”结果。
  - Configuration V（做投影向量估计但不做方位校准）出现结构缺失（文中以 Tiangong-1 太阳翼缺体素为例），说明跨帧方位尺度不一致会导致信息丢失。
  - Configuration VI（本文完整流程：投影估计 + 方位校准 + NN silhouette）达到最高/近最高 IOU（Aura 0.7358、ENVISAT 0.7258、Tiangong 0.8243；平均 0.7620），并优于 only ISAR（Configuration II）与 only optical（Configuration III）。
  - Configuration VII 用 CFAR silhouette 时 IOU 显著下降（平均约 0.4573），论文归因于轮廓一致性与完整性差。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/ecdb17dd-800c-4535-a007-1905f23d3baf" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/1f0fce7f-cf39-4680-9de7-49ea14f43865" width="360" /></td>
  </tr>
</table>

表Ix不同配置下的三维重建结果。 表X不同配置下的重构Iou。


<img src="https://github.com/user-attachments/assets/563fd930-71a1-4102-a45c-252a9f61ab2d" width="360" />
<img src="https://github.com/user-attachments/assets/cd109afa-bfc7-4f0b-a28a-a19e89efe8a5" width="360" />

图20 .不同构型下的自旋目标重构结果。第一列是Aura，第二列是微波遥感卫星，第三列是Tiangong - 1。8行代表8种不同的配置，详见表IX。


## E5. 证明方法对帧数与投影误差具有可量化的适用边界
- 目的：量化 joint 帧数、silhouette 类型、视角误差对 voxel IOU 的影响。
- 设置：在 Configuration VI 下改变 joint 帧数 $`F`$（从满足分割有效的 20 帧中抽取），并在全视角大规模仿真数据上重复实验 15 次；视角误差从 $`1^\circ`$ 到 $`5^\circ`$；对比 CFAR vs NN silhouette。
- 对比：不同 $`F`$、不同 silhouette、不同视角误差曲线。
- 结论：
  - Table XI 显示随 $`F`$ 增加 IOU 上升，约在 $`F=10`$ 时三目标 IOU 可达 $`\ge 0.7`$ 量级；继续增加后提升趋缓，论文归因于固定阈值 thr、silhouette 误差与单次过站信息有限。
  - Fig. 21 显示 NN silhouette 曲线显著优于 CFAR；当总图像帧数 $`\ge 20`$（即 $`F\ge 10`$）且视角误差 $`\le 2^\circ`$ 时，IOU 可超过 0.7（图中红虚线门限）。
  - 结论部分进一步总结：当 joint 帧数大于 10、视角误差小于 $`2^\circ`$ 时，可达到 voxel IOU $`>0.72`$。

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/c79e72ea-06ec-4292-9dd9-1e9fdc5c833d" width="360" /></td>
    <td><img src="https://github.com/user-attachments/assets/5fb46829-0385-4de2-a425-20aba8ad8f43" width="360" /></td>
  </tr>
</table>

表XI三维重建Iou与不同Isar -光学观测框架的联合f .
图21。不同图像帧数、视角误差、剪影类型下的三维重建IOU曲线。( a ) - ( c )使用CFAR剪影分别绘制了Aura，微波遥感卫星和Tiangong - 1的IOU曲线。使用NN预测的轮廓，分别绘制了Aura、微波遥感卫星和Tiangong - 1的( d ) - ( f ) IOU曲线。

---

# F. 对比结论与复盘
## F1. 作者声称的核心贡献点
- 贡献 1：采用编码器–解码器分割网络与平行四边形几何先验实现自动结构特征提取，并用 NN 预测结构级 silhouette 替代 CFAR/人工。
- 贡献 2：用最小二乘优化替代 PSO 等策略，实现对自旋目标动态参数（姿态/投影向量/有效旋转相关量）的稳健估计，扩展投影关系类 3-D 重建到自旋场景。
- 贡献 3：提出统一“等效相机投影矩阵”的 silhouette 体素重建框架，融合校准后的 ISAR 与光学结构轮廓，实现结构级 3-D 体素重建。

## F2. 痛点—解决—证据
- 痛点（来自 B1）：仅靠 ISAR 难以确定自旋目标投影关系与动态姿态。
  - 对应解决（来自 D2+D4）：用 joint 图像对的长/短边投影长度最小二乘解 $`\mathbf{s}_l,\mathbf{s}_s`$，进而解 $`\mathbf{k}_{\mathrm{radar},d}`$ 与 $`\|\boldsymbol{\omega}_{\mathrm{eff}}\|`$，并做跨帧投影对齐与方位尺度校准。
  - 证据（来自 E4）：Configuration VI 显著优于未估计/未校准的配置（IV/V），平均 IOU 达 0.7620。

- 痛点（来自 B2）：光学纹理不足导致传统特征匹配 3-D 方法不稳。
  - 对应解决（来自 D5）：用 silhouette（SFS）统一处理 ISAR 与光学，避免依赖纹理特征匹配。
  - 证据（来自 E3）：三轴稳定条件下 only optical 与 joint 均可获得 $`>0.6`$ 的 voxel IOU，而 only ISAR 失败，体现 silhouette+互补视角对几何信息的重要性。

- 痛点（来自 B3）：散射点提取/关联困难且易受各向异性与遮挡影响。
  - 对应解决（来自 D3+D5）：直接学习结构级轮廓并以体素一致性累积重建，避免散射点关联链条。
  - 证据（来自 E1+E4）：Deeplabv3+ solar panel IOU $`>0.87`$，且 NN silhouette 用于重建显著优于 CFAR silhouette（Configuration VI vs VII）。

## F3. 局限性/未来工作
- 局限性：算法适用于具有矩形太阳翼的目标，且要求 ISAR 与光学成像质量相对较高；分割模型在特定角度存在坏例，实验中需要剔除明显错误帧。
- 未来工作：将视角误差与非理想成像条件纳入 joint 优化；并通过为其他结构（如圆柱、椭球）设计特征提取扩展适用性。


## 2. 缺失信息处理记录
- 光学图像的结构分割/轮廓获取方式：文中将光学投影长度特征视为已知，并未给出光学结构分割网络或具体提取流程细节。（检索 Sec. III-A, Eq. (15) 附近；Sec. V-C 表述“optical image (assumed to be known)”）
- 体素网格参数（$`D_x,d_x`$ 等）、阈值 $`\mathrm{thr}`$ 的统一选取原则：文中在实验中给出 $`\mathrm{thr}=95\%`$ 最大累积值，但未给出 $`D_x,d_x`$ 的具体数值与对不同目标的统一设置细节。（检索 Sec. IV-B, Eq. (33)；Sec. V-D 对 thr 的说明）
