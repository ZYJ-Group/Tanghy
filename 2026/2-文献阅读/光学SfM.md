# SfM 发展脉络代表性文献

---

## 1) 可匹配性与鲁棒估计（局部特征 + 外点鲁棒）

- **Fischler & Bolles, 1981 — RANSAC**
  - DOI(ACM): https://dl.acm.org/doi/10.1145/358669.358692
  - PDF: https://www.cs.ait.ac.th/~mdailey/cvreadings/Fischler-RANSAC.pdf

- **Lowe, 2004 — SIFT (IJCV)**
  - Springer: https://link.springer.com/article/10.1023/B:VISI.0000029664.99615.94
  - PDF(author mirror): https://www.cs.ubc.ca/~lowe/papers/ijcv04.pdf

---

## 2) 大规模与 BA 工程化（从“能解”到“能解大规模”）

- **Schönberger & Frahm, 2016 — Structure-from-Motion Revisited (CVPR)**
  - CVF PDF: https://openaccess.thecvf.com/content_cvpr_2016/papers/Schonberger_Structure-From-Motion_Revisited_CVPR_2016_paper.pdf

- **Snavely, Seitz, Szeliski, 2006 — Photo Tourism (SIGGRAPH/TOG)**
  - DOI(ACM): https://dl.acm.org/doi/10.1145/1141911.1141964
  - PDF: https://phototour.cs.washington.edu/Photo_Tourism.pdf

- **Agarwal et al., 2010 — Bundle Adjustment in the Large (ECCV)**
  - Project (BAL): https://grail.cs.washington.edu/projects/bal/
  - PDF: https://grail.cs.washington.edu/projects/bal/bal.pdf

---

## 3) 稠密化（MVS 主线：从稀疏点云到稠密几何）

- **Furukawa & Ponce — PMVS / patch-based MVS（经典稠密化里程碑）**
  - PDF(mirror): https://www.cvl.iis.u-tokyo.ac.jp/class2017/2017w/papers/5.3DdataProcessing/Furukawa_Multiview_pami08a.pdf

- **Schönberger et al., 2016 — Pixelwise View Selection for Unstructured MVS（COLMAP MVS 核心）**
  - PDF(author page): https://demuc.de/papers/schoenberger2016mvs.pdf

---

## 4) 直接法与弱纹理补救（用光度一致性替代“特征可匹配性”）

- **Engel et al., 2014 — LSD-SLAM (ECCV)**
  - PDF(author): https://jakobengel.github.io/pdf/engel14eccv.pdf

- **Engel et al., 2016 — DSO (arXiv / later PAMI)**
  - arXiv: https://arxiv.org/abs/1607.02565
  - PDF(author): https://jakobengel.github.io/pdf/DSO.pdf

---

## 5) 学习特征 / 学习匹配（从手工不变性到数据驱动关联）

- **DeTone et al., 2018 — SuperPoint (CVPRW)**
  - CVF PDF: https://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w9/DeTone_SuperPoint_Self-Supervised_Interest_CVPR_2018_paper.pdf
  - arXiv: https://arxiv.org/abs/1712.07629

- **Sarlin et al., 2020 — SuperGlue (CVPR)**
  - CVF PDF: https://openaccess.thecvf.com/content_CVPR_2020/papers/Sarlin_SuperGlue_Learning_Feature_Matching_With_Graph_Neural_Networks_CVPR_2020_paper.pdf
  - arXiv: https://arxiv.org/abs/1911.11763

---

## 6) 神经场与可微渲染（表示与优化合一：可微反演）

- **Mildenhall et al., 2020 — NeRF (ECCV)**
  - ECCV/ECVA PDF: https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123460392.pdf
  - arXiv: https://arxiv.org/abs/2003.08934

- **Lin et al., 2021 — BARF (ICCV)（把“NeRF + BA”显式打通）**
  - CVF PDF: https://openaccess.thecvf.com/content/ICCV2021/papers/Lin_BARF_Bundle-Adjusting_Neural_Radiance_Fields_ICCV_2021_paper.pdf
  - arXiv: https://arxiv.org/abs/2104.06405
  - Code: https://github.com/chenhsuanlin/bundle-adjusting-NeRF
    
- **3D Gaussian Splatting (SIGGRAPH 2023 / TOG)** — 新表示范式（实时渲染 + 高质量）
  - PDF(INRIA): https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/3d_gaussian_splatting_low.pdf
  - DOI(ACM): https://dl.acm.org/doi/10.1145/3592433
  - arXiv: https://arxiv.org/abs/2308.04079
  - Code: https://github.com/graphdeco-inria/gaussian-splatting
---

# 学习式多视几何（扩展清单：权威/高影响）
- **MVSNet (ECCV 2018)** — cost volume + 可微单应变换
  - CVF PDF: https://openaccess.thecvf.com/content_ECCV_2018/papers/Yao_Yao_MVSNet_Depth_Inference_ECCV_2018_paper.pdf
  - arXiv: https://arxiv.org/abs/1804.02505

- **DUSt3R (CVPR 2024)** — Dense Unconstrained Stereo（点图回归，弱化相机模型依赖）
  - CVF PDF: https://openaccess.thecvf.com/content/CVPR2024/papers/Wang_DUSt3R_Geometric_3D_Vision_Made_Easy_CVPR_2024_paper.pdf
  - arXiv: https://arxiv.org/abs/2312.14132
  - Code: https://github.com/naver/dust3r

- **MASt3R (ECCV 2024)** — Grounding Image Matching in 3D（在 DUSt3R 上强化“3D 约束下匹配”）
  - ECVA PDF: https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/09080.pdf
  - arXiv: https://arxiv.org/abs/2406.09756
  - Code: https://github.com/naver/mast3r

- **VGGT (CVPR 2025)** 
  - CVF PDF: https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_VGGT_Visual_Geometry_Grounded_Transformer_CVPR_2025_paper.pdf
  - arXiv: https://arxiv.org/abs/2503.11651
  - Code: https://github.com/facebookresearch/vggt

---

