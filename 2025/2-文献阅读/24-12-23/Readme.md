# Attentive Contextual Attention for Cloud Removal (ACA-CRNet)

This repository implements **Attentive Contextual Attention (AC-Attention)** for cloud removal in remote sensing images. Our approach improves cloud removal by capturing long-distance features and eliminating irrelevant or unimportant patterns.

---

## Paper Information

**Authors**: Wenli Huang, Ningbo University of Technology  
**Published in**: IEEE Transactions on Geoscience and Remote Sensing  
**Received**: 23 April 2024  
**Revised**: 23 August 2024  
**Accepted**: 24 September 2024  
**Published**: 3 October 2024  
**Current Version**: 18 October 2024  

**Open Source Code**: [GitHub Repository](https://github.com/huangwenwenlili/ACA-CRNet)

---

## Index Terms
- **Attentive Contextual Attention (AC-Attention)**
- **Cloud Removal**
- **Relevant Distant Context**
- **Remote Sensing Images**

## 实验细节
- **Dataset**  
  **RICE-I、RICE-II、SEN2MS-CR**
- **Baseline**  
 **pix2pix、 SpA GAN  STGAN  DSen2-CR  UnCRtainTS  Ours**




## 1. 贡献
The contributions of this article are summarized as follows:  
1. We introduce **AC-Attention**, designed to capture informative **long-distance features** and eliminate irrelevant or unimportant patterns.  
2. We integrate **AC-Attention** into our **ACA-CRNet** to improve its cloud removal capabilities and demonstrate its effectiveness.  
3. We evaluate our approach on **three diverse datasets**, yielding both visual and quantitative results that outperform existing cloud removal methods. In addition, ablation studies confirm that **AC-Attention** effectively attends to informative long-distance contexts, highlighting its adaptability and effectiveness.

---

## 2. 框架
**I. INTRODUCTION**  
**II. RELATED WORKS**  
- A. Traditional Cloud Removal Methods  
- B. Deep Learning-Based Cloud Removal Methods  

**III. METHODOLOGY**  
- A. Attentive Contextual Attention（上下文注意力）  
  1) Vanilla Attention  
  2) Attentive Contextual Attention:  
    - a) Embedding and reshaping  
    - b) Attentive matching  
    - c) Attending  
- B. Network Architecture  
  1) Architecture  
  2) Residual Block  

**IV. EXPERIMENT**  
- A. Experiment Details  
  1) Datasets  
  2) Metrics  
  3) Implementation Details  
- B. Performance of ACA-CRNet  
  1) Comparison Baselines  
  2) Quantitative Comparison With Baselines  
  3) Qualitative Comparison With Baselines  
- C. Ablation Studies  
  1) Effectiveness of Our AC-Attention  
  2) Attentive Similarity Score Analysis  

**V. CONCLUSION**  

---

## 3. 图表
### 图 1: Comparison between the CA and our proposed AC-Attention  
The first two columns show a selected query feature, marked by red stars, along with features within the top 5% similarity to the query feature, marked by magenta pentagons. The following two columns display the similarity scores for this query feature. The next two columns present the cloud removal results.  
![Fig. 1](https://github.com/user-attachments/assets/6380228d-197f-4c8e-8d5f-52052e1f0829)

---

### 图 2: Architecture of AC-Attention  
AC-Attention consists of three steps: embedding and reshaping, attentive matching, and attending.  
![Fig. 2](https://github.com/user-attachments/assets/d15d9069-6ba5-46eb-bbf0-914f55f32489)

---

### 图 3: Overview of ACA-CRNet Architecture  
(a) ACA-CRNet architecture, (b) Stem, (c) RB, (d) RACAB, and (e) Refine component. The ACA-CRNet is designed in a residual style, comprising the Stem, RBs, RACABs, and Refine modules.  
![Fig. 3](https://github.com/user-attachments/assets/226bb12f-122e-4c1e-b30c-bd82dd0a3174)

---

### 图 4: Visualization of Cloud Removal Results on RICE-I and RICE-II Datasets  
Local details are highlighted in red boxes. Zooming in is recommended for a clearer view.  
![Fig. 4](https://github.com/user-attachments/assets/74bef0a1-1110-4440-be46-bc7cb296f494)

---

### 图 5: Cloud Removal Results for Sentinel-2 Satellite Data on the SEN12MS-CR Dataset  
The Sentinel-2 data includes 13 spectral bands, with the visualization images generated using the RGB bands. Zooming in is recommended for a clearer view.  
![Fig. 5](https://github.com/user-attachments/assets/80f3963e-15fe-4f88-b727-e2f73bce388d)

---

### 图 6: Visualization Results of ACA-CRNet  
Demonstrating the effectiveness of our AC-Attention.  
![Fig. 6](https://github.com/user-attachments/assets/29318301-a159-4e14-bac1-9ad667d2ac6b)

---

### 图 7: Effectiveness of AC-Attention on Three Network Architectures  
Visualizing the top 5% similarity scores and similarity maps.  
![Fig. 7](https://github.com/user-attachments/assets/99123528-4890-4706-8566-10df3fbc0d63)

---

### 图 8: Effectiveness of AC-Attention in Established Methods  
Illustrating the impact of AC-Attention in cloud removal methods.  
![Fig. 8](https://github.com/user-attachments/assets/35e65f04-673c-4136-9459-f09819ac55c8)

---

### 图 9: Comparison of Cloud Removal Results  
Quantitative comparison results across three datasets.  
![Fig. 9](https://github.com/user-attachments/assets/cbb276ce-3cb1-40ed-8d07-c5514c58c2d4)

---

### 图 10: Publicly Available Datasets for Cloud Removal Experiments  
Used datasets for evaluating cloud removal methods.  
![Fig. 10](https://github.com/user-attachments/assets/2430398e-a01c-4ac5-b992-ea490dd8856d)

---

---

