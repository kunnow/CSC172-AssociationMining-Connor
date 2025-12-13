# CSC173 Data Mining and Analysis Project Proposal
**Student:** Shir Keilah T. Connor, 2022-5474  
**Date:** December 12, 2025

## 1. Project Title
Discovering Behavioral Patterns in Phishing Emails Using Association Rule Mining

## 2. Problem Statement
Phishing emails remain a major cybersecurity threat, exploiting human behavior through deceptive message patterns. While many existing solutions focus on classification-based detection, these approaches often lack interpretability. There is limited emphasis on understanding the underlying relationships between email characteristics that commonly appear in phishing attempts. This project addresses this gap by applying Association Rule Mining to uncover hidden and explainable patterns in phishing emails, which can support cybersecurity awareness and rule-based defenses.

## 3. Objectives
- Apply Association Rule Mining techniques to a real-world phishing email dataset.
- Identify frequent itemsets and strong association rules related to phishing behavior.
- Analyze relationships among email features that commonly occur in phishing attempts.
- Provide interpretable insights that explain phishing email structure and strategies.

## 4. Dataset Plan
- **Source:** Kaggle – Phishing Email Dataset  
  https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset  
- **Expected Size:** Thousands of email records (CEAS_08.csv)
- **Target Attributes:** Email content indicators, sender-related features, phishing label
- **Acquisition:** Publicly available dataset downloaded from Kaggle

## 5. Technical Approach
- **Data Representation:**  
  Each email will be treated as a transaction composed of feature-value items.
- **Architecture Sketch:**  
  Raw dataset → preprocessing → transactional data → frequent itemset mining → association rule generation
- **Data Mining Technique:** Association Rule Mining
- **Algorithms:**  
  - Apriori Algorithm  
  - FP-Growth (if applicable)
- **Evaluation Measures:**  
  - Support  
  - Confidence  
  - Lift  

## 6. Expected Challenges & Mitigations
- **Challenge:** High-dimensional and mixed-type features  
  **Solution:** Feature selection, discretization, and binarization
- **Challenge:** Generating too many trivial or redundant rules  
  **Solution:** Apply minimum thresholds and rule filtering strategies
- **Challenge:** Interpreting complex rule combinations  
  **Solution:** Focus on high-lift and domain-relevant rules
