# 2020 年后航天器与空间目标 ISAR 三维重建相关工作整理

---

## Three-Dimensional Geometry Reconstruction Method for Slowly Rotating Space Targets Utilizing ISAR Image Sequence

文章  
名称：Three-Dimensional Geometry Reconstruction Method for Slowly Rotating Space Targets Utilizing ISAR Image Sequence  
期刊：Remote Sensing  
作者：Zuobang Zhou，Lei Liu，Rongzhen Du，Feng Zhou  
时间：2022  
链接：https://doi.org/10.3390/rs14051144  

背景  
面向慢速旋转且自旋轴近似固定的空间目标，许多三维重建流程需要较准确的旋转参数或可形成稳定投影关系的条件。一旦旋转参数难以获得，投影关系无法可靠建立，重建容易退化或失效。  

方法  
提出基于 ISAR 图像序列能量累积的重建思路。核心做法是在三维空间中提出候选散射点，将其投影回每一帧 ISAR 图像，在目标区域内做能量累积，用跨帧一致的高能量累积来筛选真实散射点，并通过搜索与优化得到三维点云式几何结果。  

---

## Three-Dimensional Geometry Reconstruction Method from Multi-View ISAR Images Utilizing Deep Learning

文章  
名称：Three-Dimensional Geometry Reconstruction Method from Multi-View ISAR Images Utilizing Deep Learning  
期刊：Remote Sensing  
作者：Zuobang Zhou，Xiangguo Jin，Lei Liu，Feng Zhou  
时间：2023  
链接：https://doi.org/10.3390/rs15071882  

背景  
多视角 ISAR 图像中散射特征会随视角变化出现与消失，导致传统依赖显式散射点关联与轨迹跟踪的方法不稳，同时对运动模型假设较强。工程上希望在关联不稳定时仍能恢复可用的三维结构。  

方法  
用深度学习关键点检测获得更鲁棒的可用特征，再结合多视角几何求解投影关系，并把三维重建转化为优化问题。随后通过将候选三维点投影回图像并结合能量判别来稠密化点云，输出更完整的三维几何表示。  

---

## PP-ISEA: An Efficient Algorithm for High-Resolution Three-Dimensional Geometry Reconstruction of Space Targets Using Limited Inverse Synthetic Aperture Radar Images

文章  
名称：PP-ISEA: An Efficient Algorithm for High-Resolution Three-Dimensional Geometry Reconstruction of Space Targets Using Limited Inverse Synthetic Aperture Radar Images  
期刊：Sensors  
作者：Rundong Wang，Weigang Zhu，Chenxuan Li，Bakun Zhu，Hongfeng Pang  
时间：2024  
链接：https://doi.org/10.3390/s24113550  

背景  
能量累积类三维重建方法在高分辨率条件下可能需要较多图像与较长计算时间。工程上常常只能获得有限数量的 ISAR 图像，希望在输入帧数受限时仍能高效重建。  

方法  
提出分区并行的三维重建框架，并引入排序能量半累积以更有效利用有效信息。采用先粗后细的两阶段搜索策略提升搜索效率，减少计算开销，在有限帧输入下完成三维几何重建。  

---

## RaNeRF: Neural 3-D Reconstruction of Space Targets From ISAR Image Sequences

文章  
名称：RaNeRF: Neural 3-D Reconstruction of Space Targets From ISAR Image Sequences  
期刊：IEEE Transactions on Geoscience and Remote Sensing  
作者：Afei Liu，Shuanghui Zhang，Chi Zhang，Shuaifeng Zhi，Xiang Li  
时间：2023  
链接：https://ui.adsabs.harvard.edu/abs/2023ITGRS..6198067L/abstract  

背景  
仅依赖 ISAR 图像序列进行三维重建时，传统计算机视觉式的特征提取与匹配往往缺乏稳定的成像相似性证据，导致显式对应链路不稳。需要一种不依赖手工对应的端到端重建路径。  

方法  
将目标三维结构表示为连续的神经隐式场，并建立三维结构到二维 ISAR 观测的可微关系，使得可以通过优化使渲染得到的 ISAR 图像与观测序列一致。这样绕开显式特征关联，直接得到三维重建结果。  

---

## Space Target 3-D Reconstruction Using Votes Accumulation Method of ISAR Image Sequence

文章  
名称：Space Target 3-D Reconstruction Using Votes Accumulation Method of ISAR Image Sequence  
期刊：IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing  
作者：Dan Xu，Xuan Wang，Zhixin Wu，Jixiang Fu，Yuhong Zhang，Jianlai Chen，Mengdao Xing  
时间：2024  
链接：https://doi.org/10.1109/JSTARS.2024.3401707  

背景  
在候选三维散射点规模很大、伪散射点较多的情况下，如何判别哪些三维点在多帧上是一致被支持的是真实散射点，是三维重建的关键难题。  

方法  
结合逆投影生成候选三维散射点集合，再通过投票累积机制做一致性筛选。多帧中累计投票数高的候选点被认为是实际散射点，从而得到目标三维几何结构。  

---

## Three-Dimensional Reconstruction of Space Targets Utilizing Joint Optical-and-ISAR Co-Location Observation

文章  
名称：Three-Dimensional Reconstruction of Space Targets Utilizing Joint Optical-and-ISAR Co-Location Observation  
期刊：Remote Sensing  
作者：Wanting Zhou，Lei Liu，Rongzhen Du，Ze Wang，Ronghua Shang，Feng Zhou  
时间：2025  
链接：https://doi.org/10.3390/rs17020287  

背景  
仅用单一模态进行三维重建时，很难同时获得稳定的结构信息与姿态信息。光学与 ISAR 具有互补性，但跨模态对齐与融合本身存在难度。  

方法  
构建光学与 ISAR 共址联合观测体系获取成对数据，研究两种成像之间的对齐与融合。通过建立对齐关系并进行融合重建，提升结构恢复的完整性与鲁棒性，并为结构与姿态的联合利用提供路径。  

---

## A Novel Three-Dimensional Imaging Method for Space Targets Utilizing Optical-ISAR Joint Observation

文章  
名称：A Novel Three-Dimensional Imaging Method for Space Targets Utilizing Optical-ISAR Joint Observation  
期刊：Remote Sensing  
作者：Jia Li，Yaqi Zhang，Canbin Yin，Chen Xu，Xiaotong Zhu，Hao Fang，Qun Zhang  
时间：2025  
链接：https://doi.org/10.3390/rs17233881  

背景  
在在轨服务与故障诊断等任务中需要更完备的三维结构信息。仅依靠单一二维成像难以满足结构完整性与测量精度需求，联合观测提供了新的信息来源。  

方法  
提出面向光学与 ISAR 联合观测的三维成像方法框架，利用两类观测的互补约束进行结构恢复，并给出系统化的流程与实验验证，强调联合观测条件下三维成像的可行性与收益。  

---
