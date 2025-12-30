# Three-Dimensional Reconstruction of Target Based on Phase-Derived Technology

## Paper Information
- **Title**: Three-Dimensional Reconstruction of Target Based on Phase-Derived Technology
- **Authors**: Kaifu Hou; Huayu Fan; Quanhua Liu; Lixiang Ren; Erke Mao
- **Journal**: IEEE Transactions on Geoscience and Remote Sensing
- **Timeline**: 2024-03-14 (Received) → 2024-10-29 (Revised) → 2025-01-06 (Accepted) → 2025-02-13 (Published online) → 2025-02-21 (Current version)
- **Affiliation**: the School of Information and Electronics and the Key Laboratory of Electronic and Information Technology in Satellite Navigation, Ministry of Education, Beijing Institute of Technology

## Abstract
Three-dimensional images can accurately reflect the target’s posture and structure, providing rich feature information for spatial target recognition. However, challenges arise in image registration and phase reconstruction for interferometric inverse synthetic aperture radar (InISAR) 3-D imaging when observation perspectives significantly differ, the target size is relatively large, or the squint model is present. Therefore, we propose a target 3-D reconstruction method based on phase-derived technology. For the issue of image distortion misregistration caused by differing observation perspectives, we propose transforming the traditional image registration problem into a multiscatterer association problem by extracting target scatterer information from inverse synthetic aperture radar (ISAR) 2-D images and using the iterative closest point (ICP) algorithm to achieve scatterer association between different ISAR images. To tackle the interference phase ambiguity problem caused by large target size or squint model in InISAR 3-D imaging, we propose transforming the 3-D reconstruction problem into a 3-D positioning problem for each scatterer and achieving 3-D reconstruction through a 3-D positioning method based on phasederived angle measurement (PDAM) and phase-derived range measurement (PDRM). In cases where the extracted scatterers are generally nonideal, the nonideal scatterers can be treated as a whole, and cross correlation processing can be performed between different antennas to extract the interferometric phase. Both simulation and measured data have verified the effectiveness of the proposed method.

## Index Terms
3-D reconstruction, image registration, phase-derived technology, squint model.

## Contribution
To overcome these limitations, this article proposes a novel target 3-D reconstruction method based on phasederived technology. The proposed approach utilizes 2-D ISAR results obtained from different antennas, and achieves image registration through scatterer extraction and scatterer association methods. Subsequently, the 3-D reconstruction problem is transformed into a 3-D positioning problem for each scatterer. Specifically, the method uses phasederived angle measurement (PDAM) to obtain the azimuth and elevation angles of the scatterers, and combines the phase-derived range measurement (PDRM) results of the scatterers to calculate their coordinates, thereby realizing 3-D reconstruction of the targets. The proposed method can achieve 3-D reconstruction for targets that exceed size limits under the squint model while maintaining high imaging accuracy. Moreover, in real scenarios, scatterers usually extracted from ISAR images are nonideal scatterers. These can be treated as a whole and perform cross correlation processing between different antennas to extract the interferometric phase.

## Key Terms and Naming Conventions
| # | English term (paper) | 中文对照（建议） | Abbrev. | 用词是否统一（文中） |
|---|---|---|---|---|
| 1 | Inverse Synthetic Aperture Radar | 逆合成孔径雷达 | ISAR | 统一（多用缩写 ISAR） |
| 2 | Interferometric ISAR | 干涉ISAR（干涉逆合成孔径雷达） | — | 基本统一 |
| 3 | 3-D reconstruction / three-dimensional reconstruction | 三维重建 | 3-D | 有变体（两种写法并用） |
| 4 | Phase-derived technology | 相位派生技术 | — | 统一 |
| 5 | Interference phase / interferometric phase | 干涉相位 | — | 有变体（两种写法并用） |
| 6 | Phase difference | 相位差 | Δφ | 统一 |
| 7 | Phase unwrapping / phase unwrap | 相位解缠 | — | 有变体（名词/动词两种写法） |
| 8 | Ambiguity number | 模糊整数（2π周数） | — | 统一 |
| 9 | Squint | 斜视 | — | 统一 |
| 10 | Squint model | 斜视模型 | — | 基本统一（少量写作作 “squint imaging”） |
| 11 | Normal model | 正视模型（非斜视成像模型） | — | 统一 |
| 12 | Observation angle | 观测角 | — | 统一 |
| 13 | Azimuth angle | 方位角 | — | 统一 |
| 14 | Elevation angle | 俯仰角 | — | 统一 |
| 15 | Baseline | 基线 | — | 统一 |
| 16 | Line of sight | 视线方向 | LOS | 统一 |
| 17 | Coordinate system | 坐标系 | — | 统一 |
| 18 | Scatterer / scatterers | 散射体 / 散射点 | — | 基本统一（偶见 scattering center） |
| 19 | (Point) scattering center / scattering center | （点）散射中心 | — | 少量出现（非主术语） |
| 20 | Ideal point-like scatterer | 理想点散射体 | — | 统一 |
| 21 | Nonideal scatterer | 非理想散射体 | — | 统一 |
| 22 | Scatterer extraction | 散射点提取 | — | 统一 |
| 23 | Scatterer association | 散射体关联 | — | 统一 |
| 24 | Image registration / registration | 图像配准 / 配准 | — | 有宽松用法（registration 有时泛指） |
| 25 | Misregistration | 失配/错配（配准偏差） | — | 统一 |
| 26 | Translational misregistration | 平移失配 | — | 统一 |
| 27 | Distortion misregistration | 形变失配 | — | 统一 |
| 28 | Point cloud | 点云 | — | 统一 |
| 29 | Iterative Closest Point | 迭代最近点算法 | ICP | 统一 |
| 30 | Point cloud matching / point cloud registration | 点云匹配 / 点云配准 | — | 有变体（matching/registration 并用） |
| 31 | Nearest point / closest point | 最近点 / 最近邻点 | — | 统一（表述两种） |
| 32 | Euclidean distance | 欧氏距离 | — | 统一 |
| 33 | Rotation matrix | 旋转矩阵 | R | 统一（与 T 成对出现） |
| 34 | Translation matrix | 平移矩阵 | T | 统一 |
| 35 | Iteration | 迭代 | — | 统一 |
| 36 | Convergence | 收敛 | — | 统一 |
| 37 | Pulse compression | 脉冲压缩 | — | 统一 |
| 38 | Linear frequency modulation | 线性调频 | LFM | 统一 |
| 39 | Doppler (frequency) | 多普勒（频率） | — | 统一 |
| 40 | Range–Doppler (RD) | 距离–多普勒（成像/算法） | RD | 统一 |
| 41 | Keystone transform | Keystone 变换/校正 | — | 统一 |
| 42 | Translational motion compensation | 平移运动补偿 | — | 统一 |
| 43 | MTRC correction | MTRC 校正（距离徙动校正） | MTRC | 统一 |
| 44 | Phase-derived velocity measurement | 相位派生速度测量 | PDVM | 统一 |
| 45 | Phase-derived angle measurement | 相位派生角度测量 | PDAM | 统一 |
| 46 | Phase-derived range measurement | 相位派生距离测量 | PDRM | 统一 |
| 47 | Measurement precision | 测量精度 | — | 统一 |
| 48 | Error propagation | 误差传播 | — | 统一 |
| 49 | Signal-to-noise ratio | 信噪比 | SNR | 统一 |
| 50 | Root mean square error | 均方根误差 | RMSE | 统一 |
| 51 | Monte Carlo simulation | 蒙特卡洛仿真 | — | 统一 |
| 52 | Measured data | 实测数据 | — | 统一 |

## Framework (Section Headings Only)
- I. INTRODUCTION
- II. PRINCIPLE OF 3-D IMAGING
- III. THREE-DIMENSIONAL RECONSTRUCTION BASED ON PHASE-DERIVED TECHNOLOGY
  - A. Scatterer Association Method
  - B. Three-Dimensional Reconstruction Method
- IV. ANALYSIS OF 3-D RECONSTRUCTION ACCURACY FOR TARGETS
- V. ALGORITHM VALIDATION
  - A. Simulations
    - 1) Scatterer Association Based on ICP Point Cloud Matching
    - 2) Three-Dimensional Reconstruction Based on Phase-Derived Technology
  - B. Experiment Based on Measured Data
- VI. CONCLUSION
- REFERENCES

## Figures (Captions / Placeholders)
- **Fig. 1.** Target 3-D reconstruction geometry with three antennas. (II)  
<img src="https://github.com/user-attachments/assets/1a2a4f32-e02f-475a-b6c8-aabe126b8c76" width="520" />

- **Fig. 2.** Projection of target 3-D reconstruction geometry on XOZ plane. (III.A)  
<img src="https://github.com/user-attachments/assets/4ecec1ce-86fa-4131-a268-40d12e1a2864" width="520" />

- **Fig. 3.** Image registration result of antennas A and B. (III.A)  
<img src="https://github.com/user-attachments/assets/30bbc716-8137-4242-a995-4f0677fa17a7" width="520" />

- **Fig. 4.** Flowchart of target 3-D reconstruction based on phase-derived technology. (III.B)  
<img src="https://github.com/user-attachments/assets/0d77ed24-7f2c-489b-b352-884fe857b2ca" width="520" />

- **Fig. 5.** Analysis of (a) and (b) measurement precision. (IV)  
<img src="https://github.com/user-attachments/assets/6fbd0ed8-781b-403f-8492-122023250afe" width="520" />

- **Fig. 6.** Analysis of (a) Xk measurement precision. (b) Yk measurement precision. (c) Zk measurement precision. (d) 3-D position precision. (IV)  
<img src="https://github.com/user-attachments/assets/7731c191-6f34-44d2-ab89-3432fbee4912" width="520" />

- **Fig. 7.** 3-D model of the target composed of ideal point-like scatterers. (V.A.1)  
<img src="https://github.com/user-attachments/assets/a053e2a0-094d-4c43-8d1c-362df72e222e" width="520" />

- **Fig. 8.** ISAR images of three antennas and positions of scatterers in ISAR images with registration. (a) ISAR image of antenna A. (b) ISAR image of antenna B. (c) ISAR image of antenna C. (d) Image registration result. (V.A.1)  
<img src="https://github.com/user-attachments/assets/ba4f8f98-54ca-4ffc-870b-348eff2acea1" width="520" />

- **Fig. 9.** Reconstruction result of the proposed method. (V.A.1)  
<img src="https://github.com/user-attachments/assets/7203ebb4-cde4-4e0f-9f54-a9b4de4283eb" width="520" />

- **Fig. 10.** Model of the simulated airplane target. (a) 3-D model of the target. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target. (V.A.2)  
<img src="https://github.com/user-attachments/assets/e7617ef1-3055-4452-94e1-0909771c04e0" width="520" />

- **Fig. 11.** Imaging result of algorithm proposed in [28]. (a) 3-D reconstruction model. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target. (V.A.2)  
<img src="https://github.com/user-attachments/assets/499d7472-db7b-498e-8f58-4d8187dd3e78" width="520" />

- **Fig. 12.** Interference phase unwrapping result and real phase. (a) Antennas A and B. (b) Antenna A and C. (V.A.2)  
<img src="https://github.com/user-attachments/assets/84c7da7e-63f9-47a0-85ff-f84350bb4f31" width="520" />

- **Fig. 13.** Target 3-D reconstruction result of the proposed method. (a) 3-D reconstruction model. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target. (V.A.2)  
<img src="https://github.com/user-attachments/assets/eff20b8d-16ae-4580-aa1a-6eab6e0eb13f" width="520" />

- **Fig. 14.** (a) Experimental scene. (b) Optical image of the airplane target. (V.B)  
<img src="https://github.com/user-attachments/assets/ac72abee-01e1-469f-b658-b648bab50950" width="520" />

- **Fig. 15.** Part of process flow. (a) PDVM result of four antennas. (b) Pulse compression results. (c) Result of translational motion compensation and MTRC correction. (d) ISAR image. (V.B)  
<img src="https://github.com/user-attachments/assets/4e93f9b3-cf29-4671-b782-b83779d7db7b" width="520" />

- **Fig. 16.** Scatterers positioning result of Airbus A332 by proposed method. (V.B)  
<img src="https://github.com/user-attachments/assets/34590da1-c234-47b1-b7c3-fe3c44d2cb83" width="520" />

- **Fig. 17.** Reconstruction result of Airbus A332 by proposed method. (a) 3-D reconstruction model. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target. (V.B)  
<img src="https://github.com/user-attachments/assets/add02187-55bf-452a-ac12-73987b2a7a22" width="520" />


## TABLE
- **Tab. 1.** SIMULATION PARAMETERS OF THE IMAGING SYSTEM
<img src="https://github.com/user-attachments/assets/6622a95e-d7d7-4a0c-9d63-51f257617df3" width="520" />

- **Tab. 2.** SIMULATION PARAMETERS OF THE IMAGING SYSTEM
<img src="https://github.com/user-attachments/assets/e965c750-6163-4e87-8a1a-0f20ac1a7712" width="520" />

- **Tab. 3.** ROBUSTNESS OF THE PROPOSED METHOD
<img src="https://github.com/user-attachments/assets/9505f7b1-9204-4e4d-9b78-e59b49274cb2" width="520" />
