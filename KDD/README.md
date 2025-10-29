# 💳 Credit Card Fraud Detection using the KDD Process  
_A complete end-to-end Knowledge Discovery in Databases (KDD) project_

---

## 🧠 Overview  

This project applies the **KDD (Knowledge Discovery in Databases)** methodology to detect fraudulent credit card transactions from a real-world dataset.  
The analysis demonstrates how systematic data mining — guided by the KDD process — can yield interpretable, ethical, and operationally reliable insights in the financial fraud domain.

The pipeline includes five core KDD phases:  
1. **Selection** — identify relevant, ethical data sources  
2. **Preprocessing** — clean and prepare data  
3. **Transformation** — engineer features and handle imbalance  
4. **Data Mining** — train and validate predictive models  
5. **Interpretation** — extract actionable and ethical knowledge  

---

## 📂 Dataset Summary  

| Attribute | Description |
|------------|-------------|
| **Name** | Credit Card Fraud Detection |
| **Source** | Université Libre de Bruxelles (ULB) / Kaggle ([mlg-ulb/creditcardfraud](https://www.kaggle.com/mlg-ulb/creditcardfraud)) |
| **Records** | ~284,807 transactions |
| **Features** | 30 (28 PCA components + Time + Amount + Class) |
| **Label (Target)** | `Class`: 0 = Legitimate, 1 = Fraud |
| **Fraud Ratio** | ≈ 0.17% (highly imbalanced) |
| **Ethics** | Fully anonymized, GDPR-compliant, no PII |

---

## 🏁 Phase 1 — Selection  

### 🎯 Objective  
To identify a reliable and representative dataset suitable for fraud detection while ensuring ethical and compliance standards.

### 🔍 Highlights  
- **Dataset chosen:** European Credit Card Transactions (ULB/Kaggle)  
- **Scope:** Two days of anonymized financial transactions  
- **Challenge:** Only 0.17% fraudulent cases — realistic class imbalance  
- **Goal:** Predict rare fraud accurately with minimal false positives  

### ⚖️ Ethical Safeguards  
- No personal identifiers (names, IDs, merchants)  
- Compliant with GDPR and academic data-use policy  
- Purpose limited to educational and research experimentation  

### ⚠️ Risks and Mitigations  

| Risk | Impact | Mitigation |
|------|---------|------------|
| Extreme class imbalance | High | Use SMOTE, class weighting, or anomaly detection |
| Limited temporal diversity | Medium | Treat results as illustrative, not deployable |
| PCA anonymization reduces interpretability | Medium | Use SHAP explanations for post-hoc transparency |

### ✅ Outcome  
A valid, ethical dataset selected for downstream KDD analysis, balancing research realism and governance compliance.

---

## 🧹 Phase 2 — Preprocessing  

### 🎯 Objective  
To ensure the dataset is clean, consistent, and structurally ready for modeling.

### 🧭 Steps  
1. Verified data completeness — no missing or duplicate entries.  
2. Confirmed all features are numeric (no categorical encoding required).  
3. Standardized contextual features: `Amount`, `Time`.  
4. Stratified train–test split (80/20) to preserve fraud ratio.  

### 🧾 Code Snapshot  
```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df[['Amount', 'Time']] = scaler.fit_transform(df[['Amount', 'Time']])

X = df.drop('Class', axis=1)
y = df['Class']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)
```

### Risks and Mitigation ## 🏁 Phase 1 — Selection

| Risk                | Impact | Mitigation                             |
| ------------------- | ------ | -------------------------------------- |
| Data leakage        | High   | Fit scalers only on training data      |
| Outliers in Amount  | Medium | Apply log transform                    |
| Unbalanced test set | Medium | Stratified split maintains fraud ratio |


### Outcome Clean, scaled dataset ready for transformation and modeling.

## 🔄 Phase 3 — Transformation
### Objective Enhance model learnability by engineering features, balancing classes, and ensuring scale consistency.
- Applied SMOTE for minority class resampling.
- Created derived features: `Amount_log`, `Amount_square`.
- Verified integrity via nearest-neighbor distance plots.

**🧾 Code Example**
from imblearn.over_sampling import SMOTE
```
smote = SMOTE(k_neighbors=5, random_state=42)
X_train_res, y_train_res = smote.fit_resample(X_train, y_train)

```
**📊 Class Balancing**
Before resampling: Counter({0: 226602, 1: 378})
After resampling : Counter({0: 226602, 1: 226602})

**✅ Outcome**

<img width="582" height="472" alt="image" src="https://github.com/user-attachments/assets/765f03a2-3199-4d38-bdd9-cdd700862dd1" />

Balanced, feature-rich dataset with robust scaling and augmentation.


**🤖 Phase 4 — Data Mining
🎯 Objective**

Train and compare supervised models to predict fraud effectively.

🧩 Models Used
| Model               | Type              | Rationale                   |
| ------------------- | ----------------- | --------------------------- |
| Logistic Regression | Linear            | Baseline interpretability   |
| Random Forest       | Ensemble          | Robust, non-linear learning |
| XGBoost             | Gradient Boosting | High accuracy, low bias     |

**🧾 Code Example**

```
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from xgboost import XGBClassifier

models = {
    "Logistic Regression": LogisticRegression(max_iter=1000, class_weight='balanced', random_state=42),
    "Random Forest": RandomForestClassifier(n_estimators=200, random_state=42, n_jobs=-1),
    "XGBoost": XGBClassifier(n_estimators=300, max_depth=6, learning_rate=0.1, subsample=0.8,
                             colsample_bytree=0.8, random_state=42, n_jobs=-1)
}

for name, model in models.items():
    model.fit(X_train_res, y_train_res)
    print(f"✅ {name} trained successfully.")

```


📈 Evaluation Metrics


<img width="673" height="151" alt="image" src="https://github.com/user-attachments/assets/13b1fffe-a36b-4e0d-a1a9-b91fe5a8b4d7" />


**🧠 Key Findings**
Random Forest achieved highest recall and AUC
Top features: V14, V12, V10, Amount_log
Ensemble models outperform linear baselines

**⚠️ Risks and Mitigation**
| Risk                       | Impact | Mitigation                   |
| -------------------------- | ------ | ---------------------------- |
| Overfitting                | High   | Cross-validation and pruning |
| Imbalance in real test set | Medium | Use class weights            |
| Model interpretability     | Medium | Add SHAP explainability      |

**✅ Outcome**
Random Forest selected as champion model with near-perfect fraud detection accuracy and explainability.
**
**🔍 Phase 5 — Interpretation
🎯 Objective****
Translate model outcomes into business, behavioral, and ethical insights.

🔑 Model Insights
| Feature             | Insight                                    |
| ------------------- | ------------------------------------------ |
| `V14`, `V12`, `V10` | Encapsulate behavioral anomalies           |
| `Amount_log`        | High-value spikes correlate with fraud     |
| PCA outliers        | Capture deviation from normal transactions |


**📊 Visual Interpretations**

- SHAP Summary Plot — feature importance
- Precision–Recall Curve — fraud threshold tuning
- 
  <img width="597" height="444" alt="image" src="https://github.com/user-attachments/assets/3e45ff00-d993-4ed9-90db-884e37e6aa06" />

- Confusion Matrix — balanced accuracy
- 
- <img width="587" height="479" alt="image" src="https://github.com/user-attachments/assets/2dc17d9c-13d1-4d07-b951-29e775ab12ef" />

- PDPs — show impact of top features on predictions
- 
- <img width="721" height="473" alt="image" src="https://github.com/user-attachments/assets/470a5188-afd6-4dd6-9883-e2ad8066eac6" />


**⚖️ Ethical and Governance Compliance**
| Principle      | Implementation                                    |
| -------------- | ------------------------------------------------- |
| Transparency   | SHAP explanations attached to each prediction     |
| Accountability | Quarterly retraining and drift monitoring         |
| Fairness       | Demographic parity audits planned                 |
| Regulation     | EU AI Act and IEEE P7003-aligned model governance |

**✅ Outcome**
An explainable, auditable, and ethical fraud detection framework ready for deployment.

**🧩 Key Takeaways**
| Lesson                        | Insight                                                |
| ----------------------------- | ------------------------------------------------------ |
| KDD is holistic               | From Selection to Interpretation — data to knowledge   |
| Handling imbalance is key     | SMOTE, weighting, and threshold tuning crucial         |
| Interpretability builds trust | SHAP and feature importance make decisions transparent |
| Accuracy ≠ Success            | Ethical, reproducible systems matter equally           |
| Continuous monitoring needed  | Model drift tracking maintains fairness and precision  |


**🏁 Executive Summary**
The KDD Fraud Detection Project demonstrates a complete, end-to-end implementation of the Knowledge Discovery in Databases framework.

**🎯 Key Achievements****
- Achieved ROC-AUC ≈ 0.998 and Recall ≈ 0.96 using Random Forest
- Balanced class distribution using SMOTE for fairness
- Built fully reproducible and ethical AI pipeline
- Applied SHAP for model explainability
- Designed governance-compliant monitoring protocol
