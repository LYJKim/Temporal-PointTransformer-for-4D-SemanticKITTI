# Temporal-PointTransformer-for-4D-SemanticKITTI

## Project Overview

This project focuses on **3D–4D Point Cloud Semantic Segmentation** using PointNet and PointTransformer architectures.  
It extends the conventional 3D point cloud framework into a **4D spatio-temporal representation** by incorporating temporal information between consecutive LiDAR frames.

Based on the **SemanticKITTI dataset**, the experiments were conducted in several progressive stages:

- Reproduction of the **original 3D PointTransformer** model  
- Implementation of a **Temporal-aware 4D PointTransformer**  
- Extended experiment with **longer temporal range (t−3)**  
- **Feature-level temporal integration (Proposed Method 1)**  
- **Logit-level temporal ensemble (Proposed Method 2)**  

In addition, a **PointNet toy example** was implemented as a baseline to verify the data flow, feature extraction, and overall training pipeline of 3D point cloud models.

---

## Experiment Summary

### 1. `pointnet_toy_example/`
- Implemented a simple PointNet model for 3D point cloud classification  
- Verified MLP-based feature aggregation and data preprocessing pipeline  

---

### 2. `point-transformer_3D/`
- Implemented **3D PointTransformer** for single-frame semantic segmentation on the SemanticKITTI dataset  
- Encoder–Decoder (U-Net style) architecture  
- Evaluated metrics: Accuracy, mIoU, and Time Consistency  
- **Best Accuracy:** 0.8647  
- **Best mIoU:** 0.4763  
- **Best Time Consistency:** 0.7538  

---

### 3. `point-transformer_4D/`
- Implemented a **Temporal-aware PointTransformer** using three consecutive frames (t−2, t−1, t) as input  
- Added frame index as an additional feature and applied spatio-temporal attention  
- **Best Accuracy:** 0.7950  
- **Best mIoU:** 0.4521  
- **Best Time Consistency:** 0.9312  

---

### 4. `point-transformer_4D_t-3/`
- Extended the input to **four frames (t−3, t−2, t−1, t)**  
- Applied model lightweighting for memory efficiency and increased neighborhood size (`nsample`)  
- Observed a performance drop due to lower spatial density in temporal distribution  
- **Best Accuracy:** 0.7124  
- **Best mIoU:** 0.4213  
- **Best Time Consistency:** 0.9257  

---

### 5. `point-transformer_4D_newmethod/`
- Implemented **Proposed Method 2 (Logit-level Temporal Ensemble)**  
- Each frame is independently processed by a shared PointTransformer network  
- Temporal consistency is achieved by aligning past frame predictions using **KNN matching** and applying a weighted ensemble  
  - Temporal weights: αt−2 = 0.2, αt−1 = 0.3, αt = 0.5  
- **Best Accuracy:** 0.8830  
- **Best mIoU:** 0.4996  
- **Best Time Consistency:** 0.9545  

---

## Directory Structure

```bash
Temporal-PointTransformer-for-4D-SemanticKITTI/
├── pointnet_toy_example/           # Basic PointNet toy experiment
├── point-transformer_3D/           # 3D PointTransformer implementation
├── point-transformer_4D/           # Temporal-aware 4D PointTransformer (3-frame)
├── point-transformer_4D_t-3/       # Extended 4D model using 4-frame input
├── point-transformer_4D_newmethod/ # Logit-level temporal ensemble (Proposed Method 2)
└── README.md                       # Project documentation
```
