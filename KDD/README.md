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
'''

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
