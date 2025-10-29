# 🎓 Predicting Student Performance Using the SEMMA Methodology  

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)]()  
[![Framework](https://img.shields.io/badge/Framework-SEMMA-orange.svg)]()  
[![Tool](https://img.shields.io/badge/Tool-ScikitLearn%20%7C%20Colab-green.svg)]()  
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)]()  
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)]()  

---

## 📘 Overview  

This project applies the **SEMMA data-mining methodology** (Sample, Explore, Modify, Model, Assess) to predict whether students are **at risk of academic failure**.  
The goal is to demonstrate a structured, explainable approach to predictive modeling in the education domain.

Developed as part of **Data Mining coursework at San José State University (MSSE Program)**, this project shows how to go from raw data → insight → actionable model.

---

## 🧩 Methodology: SEMMA Framework  

| Phase | Description | Output |
|--------|--------------|---------|
| 🧪 **Sample** | Selected key variables and split dataset into training/testing subsets | Balanced 80/20 split |
| 🔍 **Explore** | Conducted exploratory data analysis (EDA) and correlation visualization | Key predictors: G1, G2, absences |
| ⚙️ **Modify** | Encoded categorical variables, created engineered features, standardized numeric data | Clean ML-ready dataset |
| 🤖 **Model** | Trained Logistic Regression, Decision Tree, and Random Forest models | Random Forest achieved best performance |
| 🎯 **Assess** | Evaluated model accuracy, recall, F1, and ROC-AUC; interpreted results | Model validated for practical deployment |

---

## 🧠 Dataset  

- **Source:** [UCI Student Performance Dataset](https://archive.ics.uci.edu/ml/datasets/Student+Performance)  
- **Instances:** 395  
- **Features:** 33 total (demographic, academic, behavioral)  
- **Target:** `at_risk` (1 = final grade < 10, else 0)

---

## 🧰 Tech Stack  

| Category | Tools Used |
|-----------|-------------|
| Language | Python (3.10+) |
| Libraries | Pandas, NumPy, Matplotlib, Seaborn, scikit-learn |
| Environment | Google Colab |
| Version Control | GitHub |
| Visualization | Seaborn, Matplotlib |

---

## 📊 Results Summary  

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|--------|-----------|------------|----------|-----------|-----------|
| Logistic Regression | 0.81 | 0.69 | 0.60 | 0.64 | 0.78 |
| Decision Tree | 0.85 | 0.73 | 0.68 | 0.70 | 0.82 |
| **Random Forest** | **0.89** | **0.81** | **0.77** | **0.79** | **0.90** |

**Top Predictors:**  
- G1 (1st period grade)  
- G2 (2nd period grade)  
- Average prior grades  
- Absences  
- Study time  

✅ Random Forest outperformed others with the highest F1 and AUC scores, making it the optimal choice for identifying at-risk students.

---

## 📈 Visual Insights  

| Visualization | Description |
|----------------|--------------|
| 📊 Histograms | Distribution of key numerical variables |
| 📉 Correlation Heatmap | Relationship between grades, absences, and risk |
| 📦 Boxplots | Absences and study time across at-risk groups |
| 🌲 Feature Importance | Random Forest feature ranking |
| 🧩 Confusion Matrix | Model classification outcomes |

*(Include screenshots from your Colab notebook in this section before committing)*

---

## 🧮 Key Learnings  

- SEMMA provides a **technical and systematic** approach to building reliable ML models.  
- Early academic indicators (`G1`, `G2`) and behavioral data (absences) are strong predictors.  
- Ethical awareness is vital — models should **support, not penalize** students.  

---

## 🧭 Next Steps  

- Integrate model predictions into a school dashboard for advisors.  
- Automate retraining every term using Airflow or Prefect.  
- Expand to multi-school datasets for higher generalizability.  

---

## 🧾 Repository Structure  




---

## 📰 Medium Article  

📘 **Full Walkthrough:**  
🔗 [Predicting Student Performance Using the SEMMA Methodology](https://medium.com/)  
*(Replace with your published Medium link)*  

---

## 🤝 Author  

**[Your Name]**  
🎓 M.S. Software Engineering, San José State University  
📧 [your.email@sjsu.edu]  
🌐 [LinkedIn Profile or Portfolio Link]  

---

## 🪪 License  
This project is released under the **MIT License**.  
You are free to use, modify, and distribute with attribution.

---

## ⭐ Acknowledgments  
Special thanks to **Dr. Prateek Sharma** and the **CMPE-272 / Data Mining** teaching team for guidance.  
Also to **SAS Institute** for the SEMMA methodology framework.  

---

### 🏁 Summary  

> **SEMMA bridges statistics and machine learning through a disciplined, evidence-based approach to model building.**  
> This project demonstrates how structured methodology + ethical AI can turn educational data into actionable insights.  
