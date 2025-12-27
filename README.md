# Discovering Behavioral Patterns in Phishing Emails Using Association Rule Mining  
**CSC172 Data Mining and Analysis Final Project**  
*Mindanao State University – Iligan Institute of Technology*  

**Student:** Shir Keilah Connor, 2022-5474  
**Semester:** AY 2025-2026 Sem 1  

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://python.org) [![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)](https://jupyter.org)

---

## Abstract
Phishing emails remain one of the most prevalent social engineering threats, exploiting human behavior rather than technical vulnerabilities. This project investigates **behavioral patterns commonly found in phishing emails** using **Association Rule Mining**, specifically the Apriori algorithm. Instead of building a predictive classifier, the study focuses on **discovering interpretable co-occurrence patterns** among phishing-related features such as urgency cues, suspicious links, sender anomalies, and deceptive language structures.

The complete workflow is implemented using four Jupyter notebooks, covering environment setup, preprocessing, exploratory data analysis (EDA), transaction encoding, and rule generation. The resulting association rules highlight frequent feature combinations that characterize phishing emails, providing insights that can support cybersecurity awareness, feature engineering, and future intelligent filtering systems.

---

## Table of Contents
- [Introduction](#introduction)
- [Related Work](#related-work)
- [Methodology](#methodology)
- [Experiments & Results](#experiments--results)
- [Discussion](#discussion)
- [Ethical Considerations](#ethical-considerations)
- [Conclusion](#conclusion)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [References](#references)

---

## Introduction

### Problem Statement
Phishing emails exploit psychological triggers such as urgency, fear, authority, and reward to deceive users into revealing sensitive information. While machine learning classifiers can detect phishing, they often function as black boxes. There is a need for transparent and interpretable techniques that explain why certain email characteristics commonly appear together in phishing attempts.

### Objectives
- Analyze phishing email features using **exploratory data analysis (EDA)**.
- Transform phishing characteristics into **transactional data**.
- Apply the **Apriori algorithm** to extract frequent itemsets.
- Generate **association rules** that reveal behavioral phishing patterns.

---

## Related Work
- **Association Rule Mining** is a classic data mining technique used to discover frequent patterns and relationships within transactional datasets [1].
- The **Apriori algorithm** efficiently identifies frequent itemsets using support-based pruning [2].
- Prior phishing studies have focused on classification; fewer works emphasize **rule-based interpretability** and behavioral pattern discovery [3].
- Rule mining has been successfully applied in cybersecurity domains such as intrusion detection and fraud analysis due to its explainability [4].

---

## Methodology

### Dataset
- **Source:** Kaggle – *New pothole detection* (Smartathon) [2][3]  
- **Size:** 9,240 labeled pothole images [2][3]  
- **Task:** Object detection (bounding boxes)  
- **Splits:** As provided by the dataset export (train/valid/test)
- **Preprocessing:** Standard YOLO resizing/augmentation pipeline during training.

### Architecture
- **Detector:** Ultralytics YOLO detection model (custom-trained weights: `best.pt`)  
- **Output:** Bounding boxes + confidence score + class label (pothole)

### Training (Notebook)
Training and evaluation are implemented in:
- `train.ipynb`

The training run in the notebook uses **50 epochs**, and produces:
- `loss_curve.png` (training/validation losses + precision/recall + mAP curves)
- `map_curve.png` (mAP summary plot)

---

## Experiments & Results

### Training Curves (50 Epochs)
> These images are generated from `train.ipynb`.

![Training Curves](images/final%20(50%20epoch)/loss_curve.png)  
![mAP Summary](images/final%20(50%20epoch)/map_curve.png)

### Metrics (from `train.ipynb`)
Ultralytics reports and common definitions:
- **mAP@0.50** = Average Precision at IoU 0.50  
- **mAP@0.50:0.95** = COCO-style average across IoU thresholds from 0.50 to 0.95 [4][6]

**Overall mAP:**
| Metric | Value |
|---|---:|
| **mAP@0.50:0.95** | **0.36** |
| **mAP@0.50** | **0.62** |
| **mAP@0.75** | **0.38** |

**mAP by Object Size:**
| Object Size | mAP@0.50:0.95 | mAP@0.50 | mAP@0.75 |
|---|---:|---:|---:|
| **Small** | 0.13 | 0.34 | 0.07 |
| **Medium** | 0.30 | 0.57 | 0.31 |
| **Large** | 0.49 | 0.77 | 0.55 |

### Demo
Inference is deployed as a notebook dashboard using `ipywidgets`:
- `pothole_detection.ipynb`

The dashboard supports:
- Start/Stop controls (responsive Stop)
- Video or webcam input
- Confidence and IoU sliders
- On-frame labels with confidence (e.g., `pothole 0.82`)
- Optional export of annotated output video

**Demo Video:** [CSC173_Connor_Final.mp4](https://drive.google.com/drive/folders/12YFozZykcpD-kANAYplqiISvTK19Qlrz?usp=sharing)

---

## Discussion
**Strengths**
- Results show strong performance for **medium/large potholes**, with lower performance for **small potholes** (a known challenge in detection due to fewer pixels and weaker features).

**Limitations**
- Small potholes and low-contrast scenes (shadows, glare, wet roads) can reduce detection reliability.
- Performance depends on dataset diversity (lighting, camera angle, road texture) and annotation quality.

**Insights**
- The per-size mAP breakdown suggests future improvements should focus on increasing small-object examples or using higher-resolution training/inference for small potholes.

---

## Ethical Considerations
- **Privacy:** Road videos may capture people/vehicles. Use data responsibly and avoid sharing identifiable information.
- **Bias / Coverage:** The dataset may not represent all road types or weather conditions equally; this can affect real-world generalization.
- **Intended Use:** This project is for pothole detection; repurposing for surveillance is discouraged.

---

## Conclusion
This project demonstrates a YOLO-based pothole detector trained on an open pothole dataset and deployed in a clean, interactive Jupyter dashboard suitable for final project presentation. The model achieves solid mAP@0.50 performance and shows higher reliability on medium/large potholes. Future work can improve small pothole detection, expand dataset diversity, and optimize inference speed for edge deployment.

---

## Installation
```bash
# 1) Clone the repository
git clone https://github.com/kunnow/CSC173-DeepCV-Connor.git
cd CSC173-DeepCV-Connor

# 2) Create and activate a virtual environment
python -m venv venv
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# 3) Install dependencies
pip install -r requirements.txt
```

---

## Usage

### 1) Training
Open and run:
- `train.ipynb`

This produces training outputs and weights in the Ultralytics `runs/` directory, including:
- `runs/detect/train/weights/best.pt`

### 2) Inference Dashboard
Open and run:
- `pothole_detection.ipynb`

Inside the notebook:
1. Set `best.pt` path (or copy it to project root)
2. Choose video file (e.g., `demo.mp4`) or webcam
3. Click **Start**
4. Click **Stop** to end safely

---

## Project Structure
```txt
CSC173-DeepCV-Connor/
├─ dataset/                               # gitignored
│  └─ New-pothole-detection-2/
│
├─ images/
│  ├─ final_50_epoch/
│  │  ├─ loss_curve.png
│  │  └─ map_curve.png
│  └─ initial_10_epoch/
│     ├─ loss_curve.png
│     └─ map_curve.png
│
├─ notebooks/
│  ├─ pothole_detection.ipynb
│  └─ train.ipynb
│
├─ videos/
│  ├─ pothole_demo1.mp4
│  └─ pothole_demo2.mp4
│
├─ weights/
│  ├─ 10_epoch/
│  │  └─ best.pt
│  └─ 50_epoch/
│     ├─ best.pt
│     └─ last.pt
│
├─ .gitignore
├─ best.pt                                 # trained weights
├─ demo.mp4                                # test video
├─ progress.md
├─ proposal.md
├─ README.md
└─ requirements.txt
```

---

## References
[1] Agrawal, R., Imieliński, T., & Swami, A. “Mining Association Rules between Sets of Items in Large Databases,” SIGMOD, 1993.
[2] Han, J., Kamber, M., & Pei, J. Data Mining: Concepts and Techniques, Morgan Kaufmann.
[3] Abu-Nimeh et al., “A Comparison of Machine Learning Techniques for Phishing Detection,” ACM eCrime, 2007.
[4] Sommer, R., & Paxson, V. “Outside the Closed World: On Using Machine Learning for Network Intrusion Detection,” IEEE S&P, 2010.