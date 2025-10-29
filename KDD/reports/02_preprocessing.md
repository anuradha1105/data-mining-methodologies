# KDD Phase 2: Preprocessing

## Objective
The Preprocessing phase focuses on cleaning, validating, and preparing the selected dataset so it can be safely used for transformation and data mining. This is critical in fraud analytics because even small data quality issues can lead to biased or misleading patterns.

## 1. Data Quality Review
- Dataset size after load: [TOTAL_ROWS] rows, [TOTAL_COLS] columns.
- Data types: all features are numeric, which simplifies downstream modeling.
- Missing values: no missing values were found in any column.
- Duplicates: [DUP_COUNT] duplicate rows were detected and removed.
- Constant columns: none detected (no zero-variance features).

## 2. Target Class Imbalance
We examined the distribution of the target label `Class`:
- `Class = 0` → normal transactions
- `Class = 1` → fraudulent transactions (positive class)

Fraud cases represent approximately **[FRAUD_PCT]%** of all records.

This is an extremely imbalanced dataset. A naive classifier can get very high accuracy by predicting “not fraud” for everything, which is unacceptable. Because of this:
- Accuracy alone will NOT be used as the primary success metric.
- We will rely on Precision, Recall, F1, and ROC-AUC in later phases.

## 3. Scaling and Normalization
Although most features (`V1`–`V28`) are already PCA-transformed, `Amount` and `Time` were left in raw scale.

We standardized these with `StandardScaler`:
- `Amount` → scaled
- `Time` → scaled

This ensures that downstream models (e.g., Logistic Regression) are not dominated by raw magnitude differences.

## 4. Train/Test Split
We created an 80/20 stratified split to preserve fraud ratio and avoid information leakage.

Train shape: (226980, 30)
Test shape: (56746, 30)
Fraud % train: 0.16653449643140364
Fraud % test : 0.16741268107003138

This split locks in an unbiased test set for later evaluation.

## 5. Risks and Notes
- High class imbalance will require resampling or class weighting.
- Even tiny shifts in fraud patterns can break a model, so retraining cadence matters.
- Anonymized PCA features mean interpretability is limited — we can measure "what", not always "why".

## Next Step
Proceed to **KDD Phase 3: Transformation**, where we will address class imbalance (e.g., SMOTE / undersampling), engineer derived features, and potentially reduce dimensionality.
