# 目录
- [🎯 A. 背景与问题定义](#a-背景与问题定义)
- [⚠️ B. 核心痛点——为什么传统方法不行](#b-核心痛点为什么传统方法不行)
- [🧭 C. 作者整体思路：总体框架](#c-作者整体思路总体框架)
- [🧩 D. 具体方法](#d-具体方法)
- [📊 E. 实验与结果](#e-实验与结果)
- [✅ F. 对比结论与复盘](#f-对比结论与复盘)

# A. 背景与问题定义

## A1. 论文到底在解决什么任务

这篇论文做的是**单张图像驱动的、视觉对齐的 3D 物体重建**：给定一张自然图像里某个目标物体，模型不仅要补出它的 3D 形状，还要恢复纹理，以及它在相机坐标系中的旋转、平移和尺度。作者把它写成一个条件生成问题，而不是单一确定性回归，因为从 3D 到 2D 的拍照过程本身就是有信息损失的。 (Sec. 2.1, Fig. 1)

- 输入：
  - $`I`$：输入图像
  - $`M`$：目标物体的二值 mask
- 输出：
  - $`S`$：3D 形状
  - $`T`$：纹理
  - $`R`$：旋转
  - $`t`$：平移
  - $`s`$：尺度
- 来源：(Sec. 2.1)

- 关键公式：

```math
q(S, T, R, t, s \mid I, M) \approx p(S, T, R, t, s \mid I, M)
```

- 含义：学习一个条件生成模型，尽量逼近“给定图像和目标区域后，真实 3D 形状、纹理与布局”的条件分布。
- 符号：
  - $`I`$：输入图像
  - $`M`$：目标 mask
  - $`S`$：形状
  - $`T`$：纹理
  - $`R`$：旋转
  - $`t`$：平移
  - $`s`$：尺度
- 来源：(Sec. 2.1)

## A2. 作者假设的场景、观测条件与任务价值

作者关心的不是干净白底图，而是**真实自然图像**：目标可能很远、被遮挡、处在杂乱背景里，很多时候单看 crop 并不够，必须结合整张图里的上下文做识别和补全。测试时核心设定是**单张 RGB 图像**；此外模型也支持可选的 coarse scene point map，既可以来自硬件传感器，也可以来自单目深度估计。输出可以进一步解码成 mesh 或 3D Gaussian splats，并按物体级组合成完整场景。 (Sec. 2.2, Fig. 1, Fig. 2)

这件事重要，是因为它把 3D 感知从“需要多视角、受控数据或特定场景”推进到“直接面对真实世界图像”。论文明确把应用目标放在 robotics、AR/VR、gaming、film 和 interactive media 这些需要可组合 3D 资产与场景理解的方向上。 (Sec. 1, Sec. 6)

# B. 核心痛点——为什么传统方法不行

## B1. 单张自然图像上的 3D 重建，本质上是强欠定问题

传统几何方法更依赖多视角信号；但这篇论文要做的是单张图像反推完整 3D。问题在于：拍照把 3D 压成 2D 后，背面不可见、尺度与深度容易混淆、局部纹理和轮廓又常常被遮挡。作者强调，人类之所以还能从单张图像感知 3D，靠的不只是 shading/texture 这类 pictorial cues，还靠“识别”本身——先认出这是什么，再补它可能的 3D 结构。也就是说，这不是纯几何问题，而是**识别与重建耦合**的问题。 (Sec. 1)

## B2. 现有 image-to-3D 方法往往在“真实场景”这一步掉队

作者点名的核心失败点是：近来的单图 3D 方法虽然在孤立物体上已经很强，但大多训练于 isolated objects，上真实图像后会在**遮挡、杂乱背景、远距离目标**这些条件下明显失效。原因不是网络不会生成 3D，而是训练分布和测试分布差太远：训练时看的是居中、完整、易识别的单体物体，测试时却要面对自然图像里的局部可见物体。 (Sec. 1, Sec. 3.1.2)

论文用两类证据证明这个问题真实存在：

- 定性上，Figure 6 展示单物体重建时，现有方法在严重遮挡和复杂背景下更容易出现几何错误；Figure 7 和 Figure 20 展示场景级重建时，pipeline 方法和 joint scene 方法在布局、完整性与一致性上都明显弱于 SAM 3D。 (Fig. 6, Fig. 7, Fig. 20)
- 定量上，SAM 3D 在真实世界评测集 SA-3DAO 上，对 shape 和 layout 都显著超过现有方法；但在更接近孤立物体设定的 ISO3D 上，优势没有 SA-3DAO 那么夸张，说明真正拉开差距的是“进到真实场景后的鲁棒性”。 (Sec. 4.1, Table 2, Table 3)

## B3. 真正把领域卡住的，是 3D 标注数据而不是网络结构本身

作者反复强调 3D 的“数据壁垒”：自然图像配对真实 3D 标注极难规模化获取。普通标注员会画框、会分割，但不会从一张图直接建 mesh；专业 3D artist 虽然能做，但成本极高。附录里给了非常直观的标注统计：分割一个目标平均约 10 秒，候选 3D 里选最好的平均约 80 秒，而把 3D 对齐到 2.5D 场景里平均约 150 秒；如果完全由 artist 从单张图制作高质量 mesh，单个样本可从 5 分钟到 5 小时以上。 (Sec. 3.2.1, Sec. A.5, Sec. D.1)

所以作者的判断是：**不是先缺一个更大的生成模型，而是先缺一条把真实图像转成可训练 3D 数据的工业化路径。**这也直接引出了后面的 MITL 数据引擎。 (Sec. 1, Sec. 3.2.1)

# C. 作者整体思路：总体框架

## C1. 从输入到输出的主链路

作者的推理链路可以概括成两段：

1. 先用 Geometry model 从图像与 mask 里预测**粗形状 + 布局**。这里布局指的就是相机坐标下的旋转、平移和尺度。 (Sec. 2.2, Fig. 2)
2. 再把这个粗体素形状送入 Texture & Refinement model，补更细的几何细节，并生成纹理，最后解码成 mesh 或 Gaussian splats。 (Sec. 2.2, Fig. 2)

这里每一步解决的问题不同，也互相依赖：

- **crop 分支**负责给目标物体一个高分辨率、聚焦的局部视图。 (Sec. 2.2)
- **full-image 分支**补上下文和识别线索，因为自然图像里很多 3D 判断要靠场景语义。 (Sec. 2.2)
- **geometry 先行**是为了先把“它大概是什么形状、在相机前什么位置”定下来；否则后面的纹理与细节 refinement 没有稳定的 3D 支架。 (Sec. 2.2, Fig. 2)
- **texture/refinement 后接**，是在已有粗体素的 active voxels 上做更高分辨率生成，避免从零开始同时做所有事情。 (Sec. 2.2)

## C2. 从数据到能力的训练闭环

如果只看模型结构，这篇论文并不成立；它真正的主体是“**模型 + 数据引擎 + 多阶段训练**”这一整套系统。作者的整体框架是：

1. **Pre-training**：先在大规模合成孤立 3D 物体上学会形状与纹理先验。 (Sec. 3.1.1, Table 1)
2. **Mid-training**：再把合成物体 paste 到真实图像里，专门注入 mask-following、遮挡鲁棒性、layout 估计等能力。 (Sec. 3.1.2, Fig. 4, Table 1)
3. **Post-training**：最后用真实图像上的 MITL 标注、artist 标注和 preference 数据，把模型从 synthetic domain 拉到 real-world domain，并对齐到人类偏好。 (Sec. 3.2, Fig. 4, Table 1)
4. **Flywheel**：模型变好后，再反过来提升候选质量与标注通过率，继续产生更好的真实世界训练数据。 (Sec. 3.2, Fig. 10)

所以这篇论文的主线不是“设计了一个单点新模块”，而是：**先用合成数据搭底座，再用半合成数据注入真实场景技能，最后靠 MITL + 人类偏好把模型拉进真实世界。** (Sec. 3, Fig. 4)

# D. 具体方法

## D1. Geometry Model：先把粗形状和布局定下来 (Sec. 2.2, Sec. C.1)

- 输入：
  - cropped object image
  - cropped binary mask
  - full image
  - full-image binary mask
  - 可选 coarse scene point map $`P`$
- 输出：
  - coarse shape $`O`$
  - 旋转 $`R`$
  - 平移 $`t`$
  - 尺度 $`s`$

- 关键技术点：
  1) 用 DINOv2 分别编码局部 crop 与整图，既拿目标细节，也拿全局语义上下文。 (Sec. 2.2)
  2) 用 1.2B 参数的 flow transformer 做 Geometry 生成，同时建模粗体素形状和布局参数。 (Sec. 2.2)
  3) 采用 Mixture-of-Transformers，两条流分别处理 shape tokens 与 layout tokens，但在 multi-modal self-attention 里共享信息；这样既能在缺标签数据上只训某一模态，又能保持 shape 与 layout 的一致性。 (Fig. 2, Sec. C.1)
  4) 旋转采用 6D 表示，而不是四元数，后面的消融也证明这种表示更适合生成式训练。 (Sec. 2.2, Table 10)

- 流程步骤：
  1) 先编码 crop 和 full image 两套条件信号。 (Sec. 2.2)
  2) 在共享特征空间中联合 denoise shape 与 layout。 (Sec. C.1)
  3) 输出粗体素形状 $`O`$ 与 $`(R,t,s)`$，作为后续 refinement 的 3D 支架。 (Sec. 2.2, Fig. 2)

## D2. Texture & Refinement：在粗形状上补细节和纹理 (Sec. 2.2, Sec. C.5, Sec. C.6)

- 输入：
  - 图像条件 $`(I,M)`$
  - Geometry model 预测的 coarse shape $`O`$
- 输出：
  - refined shape $`S`$
  - texture $`T`$
  - 可解码的 mesh / Gaussian splats

- 关键技术点：
  1) 先从 coarse shape $`O`$ 中抽取 active voxels，再在这些位置上做 sparse latent flow generation，避免在整块稀疏 3D 空间里浪费建模容量。 (Sec. 2.2)
  2) Texture & Refinement model 是 600M 参数的 sparse latent flow transformer，负责补细几何和生成纹理。 (Sec. 2.2)
  3) 共享同一结构化 latent space 的两个解码器分别输出 mesh 与 3D Gaussian splats，便于面向不同下游格式。 (Sec. 2.2)
  4) 在 VAE 端，作者把原先“把图像特征回投到所有体素”的做法改成只回投到**当前视角可见体素**，形成 Depth-VAE，从而提升锐度并减少遮挡区域带来的错误特征聚合。 (Sec. C.6, Sec. C.6.1, Table 11)

- 流程步骤：
  1) 用 Geometry 给出的粗体素确定需要细化的 3D 区域。 (Sec. 2.2)
  2) 在这些 active voxels 上同时细化几何并生成纹理。 (Sec. 2.2, Sec. C.5)
  3) 最后解码成 mesh 或 Gaussian splats，作为物体级 3D 资产输出。 (Sec. 2.2)

## D3. 多阶段训练：先学 3D 先验，再学真实场景对齐 (Sec. 3.1, Sec. 3.2, Fig. 4, Table 1)

- 输入：
  - Iso-3DO：孤立合成 3D 物体数据
  - RP-3DO：render-paste 半合成真实场景数据
  - MITL-3DO / Art-3DO：真实图像上的模型辅助标注与 artist 标注
  - preference data：人类偏好对
- 输出：
  - 从 synthetic base model 到真实世界对齐后的最终模型

- 关键技术点：
  1) **Pre-training**：在 2.7M mesh、24 视角渲染得到的 Iso-3DO 上学 3D 形状与纹理先验。 (Sec. 3.1.1)
  2) **Mid-training**：用 RP-3DO 注入三类真实世界能力——mask-following、遮挡鲁棒性、layout estimation。作者报告 RP-3DO 总量约 6100 万样本。 (Sec. 3.1.2)
  3) **SFT**：先用 MITL 的非专家对齐标注拉近 synthetic-real gap，再用更小但更高质量的 Art-3DO 纠正美学与结构性失败，如 floaters、底部缺失、对称性缺失。 (Sec. 3.2.2)
  4) **DPO**：利用 Stage 2 里产生的 preference pairs，专门压掉“人类不喜欢但通用生成损失不容易刻画”的失败模式。 (Sec. 3.2.2, Sec. C.3)
  5) **Distillation**：为了在线应用，把 Geometry model 的 inference steps 从 25 压到 4。 (Sec. 3.2.2, Sec. C.4)

- 流程步骤：
  1) 先在大规模 synthetic 上学“会生成 3D”。 (Sec. 3.1.1)
  2) 再在半合成真实图像上学“会在遮挡和杂乱里找对目标”。 (Sec. 3.1.2)
  3) 最后在真实世界标注与偏好上学“输出更像人真正认可的 3D 结果”。 (Sec. 3.2)

## D4. MITL 数据引擎：把“不会做 3D 标注”改造成“会做 3D 选择与对齐” (Sec. 3.2.1, Fig. 5, Sec. A.1-A.6)

- 输入：
  - 真实图像与目标 mask
  - 多个候选 3D 结果，来自 retrieval、text-to-3D、image-to-3D，以及当前版本的 SAM 3D
- 输出：
  - 通过质量门槛的训练样本 $`D^{+}`$
  - 被拒绝的较差候选，用于 preference alignment 的 $`D^{-}`$

- 关键技术点：
  1) **Stage 1**：先决定“标哪个物体”，并拿到可靠的 2D mask。作者结合已有分割与人工筛选，并用 3D-oriented taxonomy 调平类别分布。 (Sec. 3.2.1, Sec. A.1)
  2) **Stage 2**：不让标注员直接建 mesh，而是让他们在 $`N`$ 个候选里做 best-of-$`N`$ 选择和打分；普通人做不了 3D 创作，但能判断“哪个更像”。 (Sec. 3.2.1, Sec. A.2)
  3) **Stage 2.5**：对模型几乎完全失败的 hard cases，转给专业 3D artists 手工建模，相当于给数据分布里原本到不了的区域“播种”。 (Sec. 3.2.1, Sec. A.3, Fig. 14)
  4) **Stage 3**：把选中的 shape 放回 2.5D 场景里，让标注员相对 point cloud 去调 $`R`$、$`t`$、$`s`$，补齐 layout 标注。 (Sec. 3.2.1, Sec. A.4, Fig. 13)
  5) 质量阈值会随迭代提高，模型变强后，MITL 产出的高质量数据也会变多，形成 flywheel。 (Sec. 3.2.2, Sec. A.6)

- 流程步骤：
  1) 先选真实图像中的目标物体。 (Sec. 3.2.1)
  2) 再从候选 3D 中选最像的 shape / texture。 (Sec. 3.2.1, Fig. 5)
  3) 然后把它对齐到 point cloud，得到布局标注。 (Sec. 3.2.1, Fig. 5)
  4) 把通过质量门槛的样本拿去做 SFT，把优劣对拿去做 DPO。 (Sec. 3.2.2, Sec. A.6)

- 数据规模：
  - 近 100 万张图像
  - 约 314 万个 untextured meshes
  - 约 10 万个 textured meshes
  - 超过 700 万对 pairwise preferences
- 来源：(Sec. 3.2.1, Sec. A.5)

## D5. 对齐与部署：DPO 去掉人不喜欢的失败模式，distillation 把推理压快 (Sec. 3.2.2, Sec. C.3, Sec. C.4)

- 输入：
  - Stage 2 产生的 preference pairs
  - SFT 后的参考模型
- 输出：
  - 更贴合人类偏好的模型
  - 更低 NFE、可在线部署的 Geometry model

- 关键技术点：
  1) DPO 不是在补会不会生成 3D，而是在补“哪些 3D 结果人会明确不喜欢”。作者明确说它特别有助于消除对称性、封闭性之类通用 flow matching 目标不容易直接表达的问题。 (Sec. 3.2.2)
  2) DPO 使用的是数据引擎里已有的离线 preference data，因此可以和 MITL 标注自然衔接。 (Sec. 3.2.2, Sec. C.3)
  3) Distillation 使用 shortcut model 方案，把 Geometry inference 所需的 function evaluations 从 25 降到 4，面向机器人等在线场景。 (Sec. 3.2.2, Sec. C.4)
  4) 附录显示 4-step shortcut 相比 25-step flow matching 带来约 10 倍速度提升，1-step 可到约 38 倍，但 4-step 更兼顾质量。 (Sec. E.8, Fig. 18)

- 流程步骤：
  1) 先用真实世界标注做 SFT，把模型从 synthetic 拉到 real-world。 (Sec. 3.2.2)
  2) 再用 preference pairs 做 DPO，把明显不符合人类偏好的结果往下压。 (Sec. 3.2.2)
  3) 最后做 distillation，在尽量少掉质量的前提下显著降推理成本。 (Sec. C.4, Fig. 18)

# E. 实验与结果

## E1. 实验主线：先证单物体，再证场景与布局，最后证训练和数据引擎确实起作用

作者的实验逻辑很清楚：

1. 先看**单物体 3D shape / texture** 能不能超过当前 image-to-3D 方法。 (Sec. 4.1)
2. 再看**真实场景里的 shape + layout 联合重建** 能不能成立，而不是只能做物体资产生成。 (Sec. 4.1)
3. 最后通过 stage-by-stage ablation、historical Elo 和 knockout，证明提升并不是偶然，而是来自多阶段训练和数据引擎。 (Sec. 4.2, Table 4, Fig. 10, Table 7)

主要评测集包括：

- **SA-3DAO**：1000 个由 3D artists 从自然图像制作并对齐的 3D GT，专门用来测真实世界单图重建。 (Sec. 4, Sec. D.1)
- **ISO3D**：补充测 shape / texture 的感知质量。 (Sec. 4)
- **Aria Digital Twin**：主要测 layout。 (Sec. 4)
- **Preference sets**：覆盖 SA-1B、MetaCLIP、LVIS、ADT 等不同分布和难度。 (Sec. D.2)

设置上，作者默认使用带 pointmap 条件的 Geometry model；没有 pointmap 的数据集就用单目深度估计去补。作者也专门说明：pointmap 对 shape / texture 影响很小，但对 translation / scale 这类 layout 评估更关键。 (Sec. 4, Sec. E.5)

## E2. 要回答的问题：单物体 shape / texture 是否真的比现有 image-to-3D 更强

- 要回答的问题：在真实自然图像里，SAM 3D 的单物体形状与纹理重建是否超过 Trellis、Hunyuan3D、Direct3D-S2、Hi3DGen、TripoSG 等方法？
- 设置：
  - shape 定量评测在 SA-3DAO 与 ISO3D 上进行。 (Sec. 4.1, Table 2)
  - texture 同时做 holistic image-to-3D 比较，以及在固定 SAM 3D shape 条件下只比较 texture 模块。 (Sec. E.2, Table 8, Fig. 9)
- 对比：
  - Trellis
  - HY3D-2.1 / HY3D-2.0
  - Direct3D-S2
  - TripoSG
  - Hi3DGen
  - Unitex（texture-only 对比）
- 结果与结论：
  - 在更关键的真实世界 SA-3DAO 上，SAM 3D 的 shape 指标是明显断层领先的：F1@0.01 为 0.2344，显著高于第二名 0.1629；vIoU 为 0.2311，高于第二名 0.1531；Chamfer 为 0.0400，远低于最强 baseline 的 0.0844；EMD 为 0.1211，也明显优于所有 baseline。这个量级说明它不是“略好一点”，而是在真实自然图像的 shape fidelity 上跨了一档。 (Table 2)
  - 在 ISO3D 这类更接近孤立物体设定的评测上，SAM 3D 基本达到或略超现有最好方法，说明它没有为了真实世界泛化而牺牲基础的单物体生成能力。 (Sec. 4.1, Table 2)
  - 人类偏好上，作者报告 SAM 3D 在真实图像单物体重建中达到至少 **5:1** 的 head-to-head 胜率。这个结果和 Table 2 的几何指标是一致的：不仅几何更准，人看起来也更像。 (Sec. 4.1, Fig. 8)
  - 纹理方面，在固定 SAM 3D shape 的 texture-only 对比里，SAM 3D 相对 Trellis、Hunyuan3D-2.1、Hunyuan3D-2.0、Unitex 的偏好率大多落在 **77.5%–89.1%** 区间，说明它的纹理优势不是靠“shape 更好顺带带来的全部收益”，而是纹理模块本身也更强。 (Fig. 9, Table 8)
- 来源：(Sec. 4.1, Table 2, Fig. 6, Fig. 8, Fig. 9, Table 8)

## E3. 要回答的问题：它是否真的能做“shape + layout”联合的真实场景重建

- 要回答的问题：SAM 3D 是否不只是会产出单个 3D 资产，而是真的能在自然图像里把物体放回正确的位置、方向和尺度，做 scene reconstruction？
- 设置：
  - 在 SA-3DAO 与 ADT 上评估 layout。 (Sec. 4.1, Table 3)
  - 比较两类 baseline：
    - pipeline 方法：先生成 3D，再用 Megapose 或 FoundationPose 做 pose
    - joint scene 方法：MIDI
- 对比：
  - Trellis + Megapose
  - HY3D-2.0 / 2.1 + FoundationPose 或 Megapose
  - SAM 3D + FoundationPose
  - MIDI
- 结果与结论：
  - 在 SA-3DAO 上，Joint SAM 3D 的 3D IoU 为 0.4254，而最强 pipeline baseline 为 0.2937；ADD-S@0.1 为 0.7232，而最强 pipeline baseline 为 0.5396。说明“直接联合生成 shape + layout”比“先生成再配姿态”的 pipeline 更稳。 (Table 3)
  - 在 ADT 上，这个优势仍然存在：Joint SAM 3D 的 3D IoU 为 0.4970，明显高于最强 pipeline 的 0.3864；ADD-S@0.1 为 0.7673，也高于最强 pipeline 的 0.6495。说明优势不只在作者自建 benchmark 上成立。 (Table 3)
  - 对 scene reconstruction 的人类偏好测试，作者报告 SAM 3D 相对 prior SOTA 达到 **6:1** 的偏好优势。 (Sec. 4.1, Fig. 8)
  - Figure 7 和 Figure 20 的定性结果说明，这种优势主要体现在三点：目标位置更靠谱、尺度更接近、多个物体拼起来更像一个 coherent scene，而不是若干漂浮资产。 (Fig. 7, Fig. 20)
  - 另外，作者还做了 test-time optimization：用 SAM 3D 的 layout 作为 proposal，再做 render-and-compare，可把 ADT 上的 3D IoU 从 0.4837 提到 0.5258，2D IoU 从 0.5143 提到 0.6487。这个结果说明 SAM 3D 本身已经提供了一个很强的初始解，后处理还能继续抬上限。 (Sec. E.3, Table 9)
- 来源：(Sec. 4.1, Table 3, Fig. 7, Fig. 8, Fig. 20, Sec. E.3, Table 9)

## E4. 要回答的问题：性能提升到底来自哪里——训练配方与数据引擎是否真的有效

- 要回答的问题：最终性能是靠某个单点模块，还是靠“pretrain → mid-train → MITL SFT → DPO → artist SFT → artist DPO”这条训练路径逐步堆出来的？
- 设置：
  - 做逐阶段累加实验。 (Table 4)
  - 做历史 Elo 追踪与扩容实验。 (Fig. 10)
  - 做训练阶段 knockout。 (Table 7)
- 对比：
  - 只 pretrain
  - 加 mid-training
  - 加 MITL-3DO SFT / DPO
  - 加 Art-3DO SFT / DPO
  - 移除 MITL、Art、DPO 的版本
- 结果与结论：
  - Table 4 显示 shape 性能几乎是**随阶段单调提升**的：F1@0.01 从 pretraining 的 0.1349 一路升到最终 0.2344；Chamfer 从 0.1036 降到 0.0400。说明每一个阶段都在补不同能力，而不是彼此冗余。 (Table 4)
  - 其中，mid-training 带来的提升很大，说明 render-paste 半合成数据确实教会了模型在真实场景里找目标、处理遮挡。 (Table 4)
  - MITL-3DO 的 SFT 与 DPO 继续提升，说明真实图像上的模型辅助标注和人类偏好对齐是必须的。 (Table 4)
  - Art-3DO 再往上推一截，说明 artist 级高质量数据对纠正常见结构性失败非常关键。 (Sec. 3.2.2, Table 4)
  - Figure 10a 显示随着 data engine 迭代推进，历史 Elo 基本持续上升；Figure 10b 显示只扩 MITL 数据也能持续变好，只是边际收益逐渐变小。这个结果直接支撑了作者的 flywheel 叙事。 (Fig. 10)
  - Table 7 的 knockout 更直接：去掉 MITL-3DO、Art-3DO 或 DPO，指标都会明显回落，证明这些阶段不是“锦上添花”，而是最终模型的必要组成。 (Table 7)
- 来源：(Sec. 4.2, Table 4, Fig. 10, Table 7)

## E5. 要回答的问题：一些关键设计是否真的有必要

- 要回答的问题：pointmap、rotation 表示、Texture 训练增强、Depth-VAE、distillation 这些设计，到底有没有实质作用？
- 设置：作者在附录给出多组 ablation。 (Sec. E.2, Sec. E.4, Sec. E.5, Sec. E.6, Sec. E.8)
- 对比与结果：
  - **pointmap**：对 shape 几乎没有决定性影响。作者报告在 LVIS 的 shape 偏好测试里，带 pointmap 与不带 pointmap 的版本各被选中 48%，说明 pointmap 主要帮助 layout，而不是 shape。 (Sec. E.5)
  - **rotation 表示**：Normalized 6D rotation 比 quaternion 和普通 6D rotation 都更好，ICP-Rot 从 17.9585 降到 14.5946，也带来更低的 Chamfer。说明布局建模里，表示方式本身会影响生成优化。 (Table 10)
  - **Texture 训练策略**：Figure 17 显示 lighting augmentation、RP-3DO 和 post-training data 都很关键，其中 lighting augmentation 影响尤其大；这说明 texture 质量不仅取决于模型，还强依赖训练数据是否做了去光照与真实场景适配。 (Sec. E.2, Fig. 17)
  - **Depth-VAE**：把视角特征只回投到可见体素后，PSNR、SSIM 提升，LPIPS 下降；再扩大训练数据后效果继续提升。说明 refinement 阶段对“如何聚合可见特征”很敏感。 (Sec. E.6, Table 11)
  - **distillation**：Geometry model 用 shortcut distillation 后，4-step 版本已能接近原本 25-step 的效果，同时显著提速，说明在线部署不是靠简单砍步数，而是靠专门的蒸馏目标。 (Sec. E.8, Fig. 18)
- 来源：(Sec. E.2, Fig. 17, Table 10, Sec. E.5, Table 11, Fig. 18)

# F. 对比结论与复盘

## F1. 作者自己声称的核心贡献

- 提出 SAM 3D：一个从单张图像预测物体 shape、texture 和 pose / layout 的 3D foundation model。 (Sec. 1, Sec. 6)
- 构建 MITL 标注流水线，在自然图像上以前所未有的规模获取 visually grounded 的 3D shape / texture / pose 数据。 (Sec. 1, Sec. 3.2.1)
- 提出一套类似 LLM 的多阶段训练范式：synthetic pretraining + semi-synthetic mid-training + real-world post-training + preference alignment，用来打破 3D 的数据壁垒。 (Sec. 1, Sec. 3)
- 释放新的真实世界 benchmark SA-3DAO，并在指标与人类偏好上显著超过现有方法。 (Sec. 1, Sec. 4, Sec. D.1)

## F2. 痛点 → 解决点 → 证据

### F2.1 3D 数据瓶颈闭环

- 痛点：自然图像配对高质量 3D GT 极难获得，普通标注员不会直接建 mesh，artist 全手工成本又太高。 (Sec. 1, Sec. 3.2.1, Sec. A.5, Sec. D.1)
- 解决点：把“直接做 3D 标注”改写成“候选 3D 排序 + 质量打分 + point-cloud 对齐”，再用 hard cases 的 artist 标注补尾部样本；模型变好后继续反哺数据引擎。 (Sec. 3.2.1, Fig. 5, Sec. A.1-A.6)
- 证据：作者最终积累近 100 万图像、约 314 万个 trainable shapes、约 10 万个 textures 和超 700 万对偏好数据；Figure 10 显示随着 data engine 迭代，Elo 持续上升。 (Sec. 3.2.1, Sec. A.5, Fig. 10)

### F2.2 自然图像遮挡与杂乱闭环

- 痛点：已有 image-to-3D 方法多在 isolated objects 上训练，遇到真实图像里的遮挡、背景杂乱和远距离目标时鲁棒性不够。 (Sec. 1, Sec. 3.1.2)
- 解决点：用 RP-3DO 做 mid-training，把合成物体 paste 到自然图像中，专门训练 mask-following、遮挡鲁棒性和 layout 估计，同时在推理时联合使用 crop 与 full-image 两种条件。 (Sec. 2.2, Sec. 3.1.2, Fig. 4)
- 证据：Table 4 中只加入 mid-training 就带来明显 shape 提升；Table 2 和 Figure 6 显示在 SA-3DAO 这种真实场景基准上，SAM 3D 对 shape 的优势远大于孤立物体基准。 (Table 4, Table 2, Fig. 6)

### F2.3 形状—布局联合建模闭环

- 痛点：很多方法更像是在做 3D 资产生成，shape 能出来，但无法稳定恢复物体在场景中的位置、方向和尺度；pipeline 式“先生成再配姿态”也容易误差累积。 (Sec. 4.1, Table 3)
- 解决点：Geometry model 一开始就联合建模 coarse shape 与 $`(R,t,s)`$，再通过 MoT 在 shape 与 layout 之间共享信息；后续 Stage 3 标注又专门补齐真实图像中的布局监督。 (Sec. 2.2, Fig. 2, Sec. C.1, Sec. 3.2.1)
- 证据：Table 3 中，Joint SAM 3D 在 SA-3DAO 和 ADT 上都显著超过 pipeline baselines 与 MIDI；Figure 7 和 Figure 20 的场景重建也更 coherent。 (Table 3, Fig. 7, Fig. 20)

### F2.4 从合成到真实的对齐闭环

- 痛点：只靠 synthetic pretraining，模型学到的是“会生成 3D”，但不等于“会在真实世界图像中生成对的人类认可的 3D”。 (Sec. 3.2.2)
- 解决点：先用 MITL-3DO 做 SFT 拉近 domain gap，再用 Art-3DO 修正高质量结构与美学细节，最后用 DPO 直接压低人类不喜欢的输出。 (Sec. 3.2.2)
- 证据：Table 4 显示从 MITL SFT、MITL DPO 到 Art-3DO SFT / DPO，指标继续逐步提升；Table 7 显示移除 MITL、Art 或 DPO 都会掉性能。 (Table 4, Table 7)

### F2.5 纹理质量与可部署性闭环

- 痛点：真实图像里的纹理受光照、模糊、mask 噪声和遮挡影响很大；同时高质量生成模型往往推理太慢。 (Sec. E.2, Sec. C.4)
- 解决点：纹理阶段使用去光照思路、lighting / mask / blur augmentation、RP-3DO 与真实世界 post-training；部署侧再对 Geometry model 做 shortcut distillation。 (Sec. C.5, Fig. 17, Sec. C.4)
- 证据：Figure 17 与 Table 8 说明 texture 训练设计和 post-training 都能显著提高偏好率；Figure 18 说明 4-step distillation 在保持较强质量的同时显著提速。 (Table 8, Fig. 17, Fig. 18)

## F3. 论文明确写出的局限性与后续方向

- 几何分辨率仍受限。Geometry model 的 coarse shape 分辨率是 $`64^3`$，再加上每个 occupied voxel 的 splat 数有限，对手、脸等高敏感细节仍可能失真。 (Sec. F)
- 布局目前是**逐物体预测**的，没有显式建模多物体之间的接触、稳定性、互相穿插或共面关系，因此场景物理一致性还有提升空间。 (Sec. F)
- 纹理预测并不知道最终 pose；对于具有旋转对称性的物体，偶尔会出现“纹理相当于把物体转到了错误方向”的问题。 (Sec. F)
- 作者明确给出的方向包括：提高输出分辨率、引入 super-resolution 或 parts-based generation、改用 implicit 3D representation，以及把布局预测升级为多物体联合建模。 (Sec. F)
