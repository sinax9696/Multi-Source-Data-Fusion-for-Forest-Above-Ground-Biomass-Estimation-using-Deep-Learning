# Multi-Source Data Fusion for Forest Above-Ground Biomass Estimation using Deep Learning

A deep learning–based multi-source data fusion framework integrating optical, SAR, climatic, and topographic data for explainable forest Above-Ground Biomass (AGB) estimation.

---

## 🧠 Overview
This repository provides the complete workflow, datasets preparation logic, and deep learning implementations developed for the study:

> **“Explaining Ecological Drivers and Management Implications of Forest Biomass: An Explainable Deep Learning Fusion of Remote Sensing and Climate Data”**

The framework integrates **multi-sensor remote sensing**, **process-based climate variables**, and **U-Net–based deep learning architectures**, coupled with **Explainable AI (XAI)**, to improve both the accuracy *and interpretability* of large-scale forest AGB estimation.

Unlike conventional biomass studies that rely on a single sensor or black-box models, this work explicitly investigates **how different ecological drivers contribute to biomass prediction**.

---

## 🌍 Study Scope
<img width="40%" alt="Study Area" src="Layout2.jpg" />   

- **Study area:** Rocky Mountains (Montana & Idaho, USA)
- **Forest type:** Temperate coniferous forests
- **Spatial resolution:** 30 m
- **Reference year:** 2016
- **Objective:** Accurate and interpretable estimation of forest AGB under complex topographic and climatic conditions

---

## ⚙️ Methodological Workflow
<img width="50%" alt="AGB Framework" src="UNETFlowchart.png" />

The modeling pipeline consists of three tightly coupled components:

### 1️⃣ Multi-Source Data Preparation
- **Optical:** Sentinel-2 (13 bands), Landsat-8 (7 bands)
- **SAR:** Sentinel-1 (VV, VH)
- **Climate:** Climate-FVS variables (temperature & precipitation descriptors)
- **Topography:** LiDAR-derived slope and aspect

All datasets are harmonized to **30 m resolution**, stacked into a **31-band data cube**, and extracted as **128×128 pixel patches**.

---

### 2️⃣ Deep Learning–Based AGB Estimation
Seven U-Net–based architectures are implemented and compared:

- U-Net
- V-Net
- ResU-Net
- Attention U-Net
- **U-Net3+**
- TransU-Net
- SWIN U-Net

**Training setup:**
- Optimizer: Adam (lr = 1e-5)
- Loss: Mean Squared Error (MSE)
- Batch size: 4
- Metrics: RMSE, MAE, R²

Three progressive **data fusion scenarios** are evaluated:

| Scenario | Input Data |
|--------|-----------|
| S1 | Sentinel-1 + Sentinel-2 |
| S2 | S1 + Climate-FVS + Topography |
| S3 | S2 + Landsat-8 |

---

### 3️⃣ Explainable AI (XAI) Analysis
To move beyond black-box predictions, two complementary XAI techniques are applied:

- **Gradient-based feature importance** (local sensitivity)
- **Permutation feature importance** (global contribution)

These analyses reveal:
- Dominant influence of **SWIR, Red, and NIR bands**
- Contextual role of climatic variables in complex terrain
- Limited contribution of Sentinel-1 C-band SAR in dense forests
- Implicit compensation for atmospheric effects in TOA reflectance

---

## 📊 Key Results

### Best Performing Model
**U-Net3+ (Full Fusion Scenario – S3)**

| Metric | Value |
|------|------|
| RMSE | 28.10 Mg/ha |
| MAE | 17.49 Mg/ha |
| R² | 0.89 |

### Key Findings
- Multi-source fusion significantly improves generalization
- Climate variables enhance performance in mountainous regions
- Landsat-8 provides complementary SWIR information
- Largest errors occur at forest edges and steep slopes

---

## 🛠️ Technical Environment
| Component | Version / Tool |
|---------|---------------|
| Python | 3.9+ |
| TensorFlow | 2.15+ |
| NumPy / SciPy / Scikit-learn | Latest |
| Rasterio / GDAL | 3.6+ |
| Google Earth Engine | Data preprocessing |
| NVIDIA GPU | RTX 3080 Ti (12 GB) |

---



---

## 🧾 Citation
If you use this repository or its methodology, please cite:

> Irannejad, S., & Bagheri, H. (2024).  
> **Explaining Ecological Drivers and Management Implications of Forest Biomass: An Explainable Deep Learning Fusion of Remote Sensing and Climate Data**.  
> *(Manuscript under review)*

---

## 📬 Contact
**Author:** Sina Irannejad: sinax9696@gmail.com    
Faculty of Civil Engineering and Transportation  
University of Isfahan, Iran  

📧 Corresponding author: h.bagheri@cet.ui.ac.ir

---

## 🪴 License
This project is licensed under the **MIT License** – free to use, modify, and share with proper attribution.

---

## 💡 Highlights
- Multi-sensor fusion for large-scale forest AGB estimation
- Integration of Climate-FVS variables into deep learning
- Systematic comparison of U-Net variants
- Explainable AI for ecological driver interpretation
- Reproducible and transferable framework for forest monitoring
---

## 👉 Data Accessibility: https://zenodo.org/records/17076354?token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6IjZhZmQxMjBmLWNhNTAtNDljOC04MjE4LWY1YzJmMzIxODI4NiIsImRhdGEiOnt9LCJyYW5kb20iOiI4ZGQyYjA1Y2FlNjliYzU5OTQzYjFlOTM3MTI4NDE0MSJ9.RqUNUl4Ttzfc_c3VHiNt7kFwWhc6RESDc3EkKl8dBACvj9dK_Gu0Hz0xwY6IPdL9tVVa66aq3Jhe6cq_pW6QkQ

