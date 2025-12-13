# Discovering Behavioral Patterns in Phishing Emails Using Association Rule Mining  
**Initial README.md – Project Plan, Dataset Choice, Architecture Sketch**

## Project Plan
This project focuses on analyzing **phishing emails** to uncover hidden and meaningful patterns using **Association Rule Mining (ARM)**. Instead of building a predictive classification model, the study aims to explore how different email characteristics frequently occur together in phishing attempts.

The primary goals include:
- Transforming phishing email data into a transactional format suitable for ARM.
- Discovering frequent itemsets that characterize phishing behavior.
- Generating interpretable association rules based on support, confidence, and lift.
- Analyzing the structure and strategies commonly used in phishing emails.

This project aligns directly with the motivation stated in the proposal.md: to emphasize **explainability and pattern discovery** in cybersecurity rather than black-box prediction.

---

## Dataset Choice
The project uses the **Phishing Email Dataset** available on Kaggle.

- **Dataset Name:** Phishing Email Dataset  
- **Source:** Kaggle  
- **URL:** https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset  
- **File Used:** `CEAS_08.csv`

Dataset characteristics:
- **Domain:** Cybersecurity / Email Security
- **Records:** Thousands of email instances
- **Format:** Structured tabular data
- **Content:** Email features, indicators, and phishing labels
- **Reason for choice:**  
  - Real-world phishing data  
  - Sufficient size for association rule mining  
  - Relevant and not outdated  
  - Suitable for transformation into transactional data  

Dataset preparation steps (planned):
- Remove irrelevant or identifier attributes
- Discretize numerical features
- Convert categorical features into item-value pairs
- Treat each email as a transaction
- Handle missing or inconsistent values

This dataset choice matches the dataset plan outlined in the proposal.md.

---

## Architecture Sketch
The project follows a **data mining–oriented architecture**, focusing on data transformation, pattern mining, and rule interpretation rather than model training.

### **1. Data Preparation Component**
Responsible for transforming raw email data into a format suitable for Association Rule Mining.

**Process flow:**
1. Load phishing email dataset (`CEAS_08.csv`)
2. Clean and filter relevant features
3. Discretize and binarize attributes
4. Construct transactional representations of emails

### **2. Association Rule Mining Component**
Responsible for discovering frequent patterns and generating rules.

**Mining pipeline:**
1. Frequent itemset generation
2. Association rule extraction
3. Rule filtering using support, confidence, and lift
4. Interpretation of phishing behavior patterns

### **Architecture Diagram (Text Sketch)**
```
Phishing Email Dataset (CEAS_08.csv) --> Data Cleaning & Preprocessing --> Transactional Dataset --> Frequent Itemset Mining (ARM) --> Association Rule Generation --> Pattern Analysis & Interpretation
```