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

<img width="624" height="141" alt="image" src="https://github.com/user-attachments/assets/26684c1f-603c-4295-8585-db4fdc899a20" />


**Top Predictors:**  
- G1 (1st period grade)  
- G2 (2nd period grade)  
- Average prior grades  
- Absences  
- Study time  


---

## 📈 Visual Insights  

| Visualization | Description |
|----------------|--------------|
| 📊 Histograms | Distribution of key numerical variables |
| 📉 Correlation Heatmap | Relationship between grades, absences, and risk |
| 📦 Boxplots | Absences and study time across at-risk groups |
| 🌲 Feature Importance | Random Forest feature ranking |
| 🧩 Confusion Matrix | Model classification outcomes |

<img width="575" height="453" alt="image" src="https://github.com/user-attachments/assets/3b0044d0-8104-4a3a-94e0-b661c897ac93" />


<img width="835" height="470" alt="image" src="https://github.com/user-attachments/assets/437d77f2-7423-49d0-b7fb-1d83f9102065" />


<img width="624" height="458" alt="image" src="https://github.com/user-attachments/assets/ce0f78cf-782e-4c65-9245-cb65d384d197" />


<img width="622" height="471" alt="image" src="https://github.com/user-attachments/assets/6c8b5ede-1441-4ea9-b971-4492f12c32d7" />



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

## 📰 Medium Article  

📘 **Full Walkthrough:**  
https://medium.com/@anuradhasrivastav25/predicting-student-performance-using-the-semma-methodology-5f4c8da59d22  

--- 
