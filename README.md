# Discovering Behavioral Patterns in Phishing Emails Using Association Rule Mining
**CSC172 Intelligent Systems Final Project**  
*Mindanao State University – Iligan Institute of Technology*  

**Student:** Shir Keilah Connor, 2022-5474
**Semester:** AY 2025–2026 Sem 1  

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://python.org) [![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)](https://jupyter.org) [![Data%20Mining](https://img.shields.io/badge/Data%20Mining-Apriori-green)](#)

---

## Abstract
Phishing emails remain one of the most prevalent social-engineering threats, leveraging both linguistic and technical cues (urgency, spoofed senders, malicious links, credential requests) to deceive recipients. This project investigates **behavioral patterns in phishing emails** using **Association Rule Mining (Apriori)** to discover interpretable co-occurrence rules among engineered phishing indicators. The analysis is executed as a reproducible **Jupyter Notebook** pipeline covering environment setup, preprocessing, EDA, transaction encoding, frequent itemset mining, and rule generation. The resulting rules provide actionable insight for feature engineering, awareness training, and rule-based triage systems.

**Dataset (Kaggle):** https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset

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
Phishing campaigns exploit predictable human behaviors and message artifacts to persuade recipients into disclosing credentials or executing unsafe actions. While classifiers detect phishing, they often lack interpretability. Association rule mining uncovers *interpretable* frequent co-occurrence patterns that explain how multiple cues combine in real phishing emails.

### Objectives
- Clean and preprocess a large public phishing/ham email corpus.  
- Engineer binary/categorical phishing indicators from text and metadata.  
- Convert emails into transactions and run Apriori to extract frequent itemsets & association rules.  
- Analyze rules by support, confidence, and lift and provide actionable observations.

---

## Related Work
- **Association Rule Mining & Apriori** are classic methods for discovering frequent patterns and association rules in transactional data [1][2].  
- Prior phishing research mostly focuses on supervised classification; interpretability-focused pattern mining remains an important complementary approach [3].  
- Rule mining is commonly used in security domains for explainable detection and triage heuristics [4].

---

## Methodology

### Dataset
- **Source:** *Phishing Email Dataset* by Naser Abdullah Alam (Kaggle).  
- **Contents:** A merged corpus (Enron, SpamAssassin, and other sources) with a large number of labeled emails (phishing/spam and ham). Place the downloaded CSV(s) under `data/raw/` (see Project Structure).  
- **Preprocessing:** deduplication, anonymization, header parsing (when available), and normalization (lowercasing, tokenization).

### Feature engineering (examples)
Each email is converted into a transaction composed of binary items (presence/absence):
- `Has_Suspicious_Link` — detected URLs with heuristics (IP in URL, suspicious TLDs, or domain mismatch).  
- `Contains_Urgent_Words` — keywords like *urgent*, *immediately*, *act now*.  
- `Requests_Credentials` — phrases requesting passwords, account verification, or SSNs.  
- `Sender_Spoofed` — suspicious sender address patterns or reply-to mismatches (where headers exist).  
- `Contains_Attachment` — attachments present (noting file types).  
- `Contains_Shortened_URL` — URL shorteners detected (bit.ly, tinyurl, etc.).  

### Notebooks & pipeline
1. `00` — environment setup and reproducibility.  
2. `01` — project entry & preprocessing (loads raw CSVs, creates `cleaned_phising.csv`).  
3. `02` — EDA and transaction encoding (`phising_transactions.csv`, `transactions.pkl`).  
4. `03` — Apriori frequent itemset mining, rule generation and export (`top_rules.csv`).

### Mining parameters & evaluation
- **Support:** tuned experimentally (example start: `min_support = 0.01`).  
- **Confidence:** starting point `min_confidence = 0.50`.  
- **Lift:** used to prioritize non-trivial rules (lift > 1.0; prefer >1.2).  
- Export results and visualize top rules and itemset co-occurrences.

---

## Experiments & Results

### Outputs produced
- `data/processed/cleaned_phising.csv` — cleaned dataset used for analysis.  
- `data/processed/phising_transactions.csv` — transaction CSV (one transaction per email).  
- `data/processed/phising_phising_only_transactions.csv` — transactions filtered to phishing labels only.  
- `data/processed/phishing_transofrmed_sample.csv` — sampled transformed transactions for quick runs.  
- `data/processed/transactions.pkl` — pickled transactions object for fast reloading.  
- `data/processed/top_rules.csv` — exported top association rules (support/confidence/lift).

### Example findings (illustrative)
- `{Contains_Urgent_Words, Has_Suspicious_Link} → Requests_Credentials` — often high confidence and lift.  
- `{Sender_Spoofed, Contains_Shortened_URL} → Has_Suspicious_Link` — frequent co-occurrence in phishing subsets.  

(Exact numeric metrics and full rule tables are available in `data/processed/top_rules.csv` and visualized by `03` notebook.)

### Demo
**Demo Video:** [CSC172_Connor_Final.mp4](https://drive.google.com/drive/folders/1LZspdn-4IoMUHfITY-nsFBrJ7mBGvMxH?usp=sharing)

---

## Discussion

### Strengths
- Results are **interpretable** and actionable for awareness materials and feature design.  
- Large multi-source dataset improves coverage of phishing tactics.

### Limitations
- Rules are **correlational**, not causal.  
- Quality of outcomes depends on preprocessing and the heuristics used for feature extraction (link detection, header parsing).  
- Some header-level signals (DKIM/SPF) may not be present in the public dataset.

### Practical application
- Seed features for supervised classifiers.  
- Implement rule-based email highlighting / triage heuristics.  
- Inform phishing simulation scenarios for training.

---

## Ethical Considerations
- **Privacy:** Anonymize email contents and metadata; remove or redact personally identifying information.  
- **Dual use risk:** Use findings to defend and educate only — do not use to craft phishing campaigns.  
- **Transparency:** Report dataset provenance and preprocessing choices when publishing results.

---

## Conclusion
This project uses Apriori association rule mining on a large Kaggle email corpus to reveal frequent behavioral patterns in phishing emails. The notebook pipeline is reproducible and produces interpretable rule sets that can inform both research (feature engineering) and practice (awareness and heuristics).

---

## Installation
```bash
# Clone the repository
git clone https://github.com/kunnow/CSC172-AssociationMining-Connor.git
cd CSC172-AssociationMining-Connor

# (Optional) Create and activate a virtual environment
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

---

## Usage

### 1) Download the Kaggle dataset
Place the CSV(s) depending on how you maintain the raw fi;es.

### 2) Run notebooks in order:
- `00-setup-and-environment.ipynb`
- `01-project-and-preprocessing.ipynb`
- `02-eda-and-transactions.ipynb`
- `03-apriori-rules-and-results.ipynb`

### 3) Outputs will be written to `data/processed/` including `top_rules.csv` and intermediate transaction files.
---

## Project Structure
```txt
CSC173-DeepCV-Connor/
├─ data/                          
│  └─ processed
│     ├─ cleaned_phising.csv
│     ├─ phising_phising_only_transactions.csv
│     ├─ phising_transactions.csv
│     ├─ phishing_transofrmed_sample.csv
│     ├─ top_rules.csv
│     └─ transactions.pkl
│
│  ├─ raw 
│     ├─ final
│     │  └─ 1 final dataset csv
│     └─ initial
│        └─ 6 initals dataset csvs 
│
├─ notebooks/
│  ├─ 00-setup-and-environment.ipynb
│  ├─ 01-project-and-preprocessing.ipynb
│  ├─ 02-eda-and-transactions.ipynb
│  └─ 03-apriori-rules-and-results.ipynb
│
├─ venv
├─ .gitattributes
├─ .gitignore
├─ progress.md                             
├─ proposal.md                       
├─ README.md
└─ requirements.txt
```

---

## References
[1] Agrawal, R., Imieliński, T., & Swami, A. “Mining Association Rules between Sets of Items in Large Databases,” SIGMOD, 1993.
[2] Han, J., Kamber, M., & Pei, J. Data Mining: Concepts and Techniques, Morgan Kaufmann.
[3] Abu-Nimeh, S., Nappa, D., Wang, X., & Nair, S. “A Comparison of Machine Learning Techniques for Phishing Detection,” ACM eCrime Research, 2007.
[4] Sommer, R., & Paxson, V. “Outside the Closed World: On Using Machine Learning for Network Intrusion Detection,” IEEE S&P, 2010.
[5] Kaggle — Phishing Email Dataset by Naser Abdullah Alam. https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset