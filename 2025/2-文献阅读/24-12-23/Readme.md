# Attentive Contextual Attention for Cloud Removal (ACA-CRNet)

This repository implements **Attentive Contextual Attention (AC-Attention)** for cloud removal in remote sensing images. Our approach improves cloud removal by capturing long-distance features and eliminating irrelevant or unimportant patterns.

---

## Paper Information

**Title**: Attentive Contextual Attention for Cloud Removal  
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

---

## 1. Contributions

The key contributions of this paper are:
1. **Introduction of AC-Attention**: Designed to capture long-distance features and eliminate irrelevant or unimportant patterns.
2. **Integration of AC-Attention into ACA-CRNet**: We demonstrate the effectiveness of AC-Attention in improving cloud removal capabilities.
3. **Evaluation on Three Diverse Datasets**: Our approach outperforms existing cloud removal methods, with both visual and quantitative results. Ablation studies further confirm the efficacy of AC-Attention in attending to informative long-distance contexts.

---

## 2. Framework

### I. Introduction
- **Motivation**: Cloud removal is crucial for high-quality remote sensing image analysis. This paper proposes a novel method for effective cloud removal by leveraging the AC-Attention mechanism.

### II. Related Works
- **A. Traditional Cloud Removal Methods**: A brief discussion on classical methods for cloud removal.
- **B. Deep Learning-Based Cloud Removal Methods**: Reviews recent advancements in deep learning techniques for cloud removal.

### III. Methodology
#### A. Attentive Contextual Attention (AC-Attention)
1. **Vanilla Attention**: Traditional attention mechanisms that focus on local regions.
2. **Attentive Contextual Attention**:
   - **a) Embedding and Reshaping**: Captures features at different spatial levels.
   - **b) Attentive Matching**: Identifies relevant distant context for cloud removal.
   - **c) Attending**: Attends to informative regions for improved prediction.

#### B. Network Architecture
1. **Architecture**: The ACA-CRNet is designed with a residual network structure, integrating the AC-Attention for optimal performance.
2. **Residual Block**: Details the residual connections used to stabilize training and improve accuracy.

---

## 3. Experiment

### A. Experiment Details
- **Datasets**:  
  - **RICE-I**  
  - **RICE-II**  
  - **SEN2MS-CR**
  
- **Metrics**: Performance is evaluated using standard cloud removal metrics.
  
- **Implementation Details**: We describe the network setup, training parameters, and data preprocessing.

### B. Performance of ACA-CRNet
1. **Comparison Baselines**:
   - **pix2pix**
   - **SpA GAN**
   - **STGAN**
   - **DSen2-CR**
   - **UnCRtainTS**
   - **Ours**
   
2. **Quantitative Comparison**:  
   Visual and quantitative results demonstrate that ACA-CRNet outperforms the baselines on all evaluated datasets.

3. **Qualitative Comparison**:  
   Visual comparison of cloud removal results highlights the effectiveness of ACA-CRNet.

### C. Ablation Studies
1. **Effectiveness of AC-Attention**:  
   Ablation studies confirm that AC-Attention significantly enhances cloud removal.
   
2. **Attentive Similarity Score Analysis**:  
   Detailed analysis of how AC-Attention improves feature matching.

---

## 4. Visualizations

### Fig. 1: Comparison of CA and AC-Attention
![Fig. 1: Comparison of CA and AC-Attention](https://github.com/user-attachments/assets/6380228d-197f-4c8e-8d5f-52052e1f0829)
- The first two columns show selected query features (red stars) and features with high similarity (magenta pentagons).
- The following columns show similarity scores and cloud removal results.

---

### Fig. 2: Architecture of AC-Attention
![Fig. 2: Architecture of AC-Attention](https://github.com/user-attachments/assets/d15d9069-6ba5-46eb-bbf0-914f55f32489)
- The AC-Attention mechanism is composed of three steps: embedding and reshaping, attentive matching, and attending.

---

### Fig. 3: Overview of ACA-CRNet
![Fig. 3: Overview of ACA-CRNet](https://github.com/user-attachments/assets/226bb12f-122e-4c1e-b30c-bd82dd0a3174)
- The ACA-CRNet architecture includes various components like Stem, RB, RACAB, and Refine.

---

### Fig. 4: Cloud Removal Results on RICE-I and RICE-II
![Fig. 4: Cloud Removal Results on RICE-I and RICE-II](https://github.com/user-attachments/assets/74bef0a1-1110-4440-be46-bc7cb296f494)
- Visual results show improved cloud removal on RICE-I and RICE-II datasets.

---

### Fig. 5: Cloud Removal Results on SEN12MS-CR Dataset
![Fig. 5: Cloud Removal Results on SEN12MS-CR](https://github.com/user-attachments/assets/80f3963e-15fe-4f88-b727-e2f73bce388d)
- Visual results for Sentinel-2 satellite data, demonstrating the effectiveness of ACA-CRNet.

---

### Fig. 6: Effectiveness of AC-Attention in ACA-CRNet
![Fig. 6: Effectiveness of AC-Attention](https://github.com/user-attachments/assets/29318301-a159-4e14-bac1-9ad667d2ac6b)
- Visualization demonstrating the impact of AC-Attention on cloud removal performance.

---

### Fig. 7: AC-Attention vs CA
![Fig. 7: AC-Attention vs CA](https://github.com/user-attachments/assets/99123528-4890-4706-8566-10df3fbc0d63)
- Comparison showing similarity scores and removal results between CA and AC-Attention.

---
