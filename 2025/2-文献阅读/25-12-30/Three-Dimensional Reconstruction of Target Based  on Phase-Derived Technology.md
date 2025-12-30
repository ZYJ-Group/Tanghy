# Three-Dimensional Reconstruction of Target Based on Phase-Derived Technology

## Paper Information
- **Title**: Three-Dimensional Reconstruction of Target Based on Phase-Derived Technology
- **Authors**: Kaifu Hou; Huayu Fan; Quanhua Liu; Lixiang Ren; Erke Mao
- **Journal**: IEEE Transactions on Geoscience and Remote Sensing
- **Received 14 March 2024; revised 29 October 2024; accepted 6 January 2025.**
- **Affiliation**: the School of Information and Electronics and the Key Laboratory of Electronic and Information Technology in Satellite Navigation, Ministry of Education, Beijing Institute of Technology

## Abstract
Three-dimensional images can accurately reflect the target’s posture and structure, providing rich feature information for spatial target recognition. However, challenges arise in image registration and phase reconstruction for interferometric inverse synthetic aperture radar (InISAR) 3-D imaging when observation perspectives significantly differ, the target size is relatively large, or the squint model is present. Therefore, we propose a target 3-D reconstruction method based on phase-derived technology. For the issue of image distortion misregistration caused by differing observation perspectives, we propose transforming the traditional image registration problem into a multiscatterer association problem by extracting target scatterer information from inverse synthetic aperture radar (ISAR) 2-D images and using the iterative closest point (ICP) algorithm to achieve scatterer association between different ISAR images. To tackle the interference phase ambiguity problem caused by large target size or squint model in InISAR 3-D imaging, we propose transforming the 3-D reconstruction problem into a 3-D positioning problem for each scatterer and achieving 3-D reconstruction through a 3-D positioning method based on phasederived angle measurement (PDAM) and phase-derived range measurement (PDRM). In cases where the extracted scatterers are generally nonideal, the nonideal scatterers can be treated as a whole, and cross correlation processing can be performed between different antennas to extract the interferometric phase. Both simulation and measured data have verified the effectiveness of the proposed method.

## Index Terms
3-D reconstruction, image registration, phase-derived technology, squint model.

## Contribution
To overcome these limitations, this article proposes a novel target 3-D reconstruction method based on phasederived technology. The proposed approach utilizes 2-D ISAR results obtained from different antennas, and achieves image registration through scatterer extraction and scatterer association methods. Subsequently, the 3-D reconstruction problem is transformed into a 3-D positioning problem for each scatterer. Specifically, the method uses phasederived angle measurement (PDAM) to obtain the azimuth and elevation angles of the scatterers, and combines the phase-derived range measurement (PDRM) results of the scatterers to calculate their coordinates, thereby realizing 3-D reconstruction of the targets. The proposed method can achieve 3-D reconstruction for targets that exceed size limits under the squint model while maintaining high imaging accuracy. Moreover, in real scenarios, scatterers usually extracted from ISAR images are nonideal scatterers. These can be treated as a whole and perform cross correlation processing between different antennas to extract the interferometric phase.

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
<img width="771" height="697" alt="image" src="https://github.com/user-attachments/assets/1a2a4f32-e02f-475a-b6c8-aabe126b8c76" />

- **Fig. 2.** Projection of target 3-D reconstruction geometry on XOZ plane.(III.A)
<img width="997" height="820" alt="image" src="https://github.com/user-attachments/assets/4ecec1ce-86fa-4131-a268-40d12e1a2864" />

- **Fig. 3.** Image registration result of antennas A and B.(III.A)
<img width="646" height="791" alt="image" src="https://github.com/user-attachments/assets/30bbc716-8137-4242-a995-4f0677fa17a7" />

- **Fig. 4.** Flowchart of target 3-D reconstruction based on phase-derived technology.
<img width="711" height="683" alt="image" src="https://github.com/user-attachments/assets/0d77ed24-7f2c-489b-b352-884fe857b2ca" />

- **Fig. 5.** Analysis of (a) and (b) measurement precision.
<img width="956" height="439" alt="image" src="https://github.com/user-attachments/assets/6fbd0ed8-781b-403f-8492-122023250afe" />

- **Fig. 6.** Analysis of (a) Xk measurement precision. (b) Yk measurement precision. (c) Zk measurement precision. (d) 3-D position precision.
<img width="952" height="842" alt="image" src="https://github.com/user-attachments/assets/7731c191-6f34-44d2-ab89-3432fbee4912" />

- **Fig. 7.** 3-D model of the target composed of ideal point-like scatterers.
<img width="959" height="751" alt="image" src="https://github.com/user-attachments/assets/a053e2a0-094d-4c43-8d1c-362df72e222e" />

- **Fig. 8.** ISAR images of three antennas and positions of scatterers in ISAR images with registration. (a) ISAR image of antenna A. (b) ISAR image of antenna B. (c) ISAR image of antenna C. (d) Image registration result.
<img width="963" height="838" alt="image" src="https://github.com/user-attachments/assets/ba4f8f98-54ca-4ffc-870b-348eff2acea1" />

- **Fig. 9.** Reconstruction result of the proposed method.
<img width="712" height="598" alt="image" src="https://github.com/user-attachments/assets/7203ebb4-cde4-4e0f-9f54-a9b4de4283eb" />

- **Fig. 10.** Model of the simulated airplane target. (a) 3-D model of the target. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target.
<img width="1030" height="856" alt="image" src="https://github.com/user-attachments/assets/e7617ef1-3055-4452-94e1-0909771c04e0" />

- **Fig. 11.** Imaging result of algorithm proposed in [28]. (a) 3-D reconstruction model. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target.
<img width="991" height="868" alt="image" src="https://github.com/user-attachments/assets/499d7472-db7b-498e-8f58-4d8187dd3e78" />

- **Fig. 12.** Interference phase unwrapping result and real phase. (a) Antennas A and B. (b) Antenna A and C.
<img width="949" height="429" alt="image" src="https://github.com/user-attachments/assets/84c7da7e-63f9-47a0-85ff-f84350bb4f31" />

- **Fig. 13.** Target 3-D reconstruction result of the proposed method. (a) 3-D reconstruction model. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target.
<img width="994" height="844" alt="image" src="https://github.com/user-attachments/assets/eff20b8d-16ae-4580-aa1a-6eab6e0eb13f" />

- **Fig. 14.** (a) Experimental scene. (b) Optical image of the airplane target.
<img width="1038" height="586" alt="image" src="https://github.com/user-attachments/assets/ac72abee-01e1-469f-b658-b648bab50950" />

- **Fig. 15.** Part of process flow. (a) PDVM result of four antennas. (b) Pulse compression results. (c) Result of translational motion compensation and MTRC correction. (d) ISAR image.
<img width="959" height="841" alt="image" src="https://github.com/user-attachments/assets/4e93f9b3-cf29-4671-b782-b83779d7db7b" />

- **Fig. 16.** Scatterers positioning result of Airbus A332 by proposed method.
<img width="494" height="406" alt="image" src="https://github.com/user-attachments/assets/34590da1-c234-47b1-b7c3-fe3c44d2cb83" />

- **Fig. 17.** Reconstruction result of Airbus A332 by proposed method. (a) 3-D reconstruction model. (b) Top view of the target. (c) Front view of the target. (d) Side view of the target.
<img width="701" height="608" alt="image" src="https://github.com/user-attachments/assets/add02187-55bf-452a-ac12-73987b2a7a22" />
