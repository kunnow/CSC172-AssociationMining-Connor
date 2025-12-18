# CSC172 Association Rule Mining – Progress Report

**Project Title:** Discovering Behavioral Patterns in Phishing Emails Using Association Rule Mining
**Student:** Shir Keilah T. Connor, 2022-5474
**Course:** CSC172 – Association Rule Mining
**Repository:** [https://github.com/kunnow/CSC172-AssociationMining-Connor](https://github.com/kunnow/CSC172-AssociationMining-Connor)

---

## 1. Project Objective

This project applies **Association Rule Mining (ARM)** to a phishing email dataset to uncover **recurrent behavioral patterns** commonly used in phishing attacks. By transforming email content into transactional data, the study aims to extract interpretable rules that characterize phishing behavior and support cybersecurity analysis.

---

## 2. Dataset Description

* **Dataset:** *Phishing Email Dataset* (Kaggle – Naser Abdullah Alam)
* **Source:** [https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset](https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset)
* **Format:** CSV
* **Key columns:**

  * `text` / `body` – email content
  * `label` – phishing (1) or legitimate (0)
* **Total emails processed:** [insert count]

Each email is treated as **one transaction** after feature extraction.

---

## 3. Feature Engineering & Preprocessing

### Engineered Behavioral Features (Items)

* **Language cues:** urgent_terms, threat_language, reward_language
* **URL indicators:** contains_url, suspicious_link, shortened_url
* **Sender traits:** unknown_sender, spoofed_domain
* **Email structure:** html_email, has_attachment
* **Action requests:** credential_request, verify_account, click_link

### Preprocessing Steps

* Cleaned and validated raw email text
* Extracted binary behavioral indicators from content
* Converted each email into a transactional itemset
* Applied one-hot encoding for ARM compatibility

**Sample Transaction:**
`contains_url, urgent_terms, credential_request, unknown_sender`

---

## 4. Exploratory Data Analysis (EDA)

* **Average indicators per email:** [value]
* **Most frequent indicator:** [feature] (support = [value])
* High sparsity observed due to high-dimensional feature space

EDA visualizations include feature frequency distributions and transaction-size histograms.

---

## 5. Association Rule Mining Implementation

* **Algorithm:** Apriori
* **min_support:** [value from code]
* **min_confidence:** [value from code]
* **Evaluation metrics:** support, confidence, lift

Frequent itemsets and association rules are generated to identify common co-occurring phishing behaviors.

---

## 6. Challenges Encountered

| Challenge           | Mitigation                        |
| ------------------- | --------------------------------- |
| Sparse transactions | Support threshold tuning          |
| Noisy text features | Feature filtering and grouping    |
| Weak rules          | Pruning using lift and confidence |

---

## 7. Next Steps

* Finalize Apriori parameters
* Extract top high-lift rules
* Interpret behavioral phishing patterns
* Generate rule visualizations
* Finalize README and presentation

---

**Status:** On track for final submission
