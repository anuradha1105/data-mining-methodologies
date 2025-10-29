# KDD Phase 3: Transformation

## Objective
The Transformation phase prepares the preprocessed dataset for data mining by resolving class imbalance, normalizing features, and optionally reducing dimensionality.

## 1. Resampling
- Method: SMOTE (Synthetic Minority Over-Sampling Technique)  
Before resampling: Counter({0: 226602, 1: 378})
After resampling : Counter({0: 226602, 1: 226602})

SMOTE generated synthetic fraud samples to balance the dataset. This avoids biasing models toward the majority class.

## 2. Feature Scaling
`Amount` and `Time` were already standardized in preprocessing and retained for modeling.

## 3. Dimensionality Reduction
Applied PCA (n_components = 2) to visualize data structure.
The projection shows partial separation between fraudulent and legitimate clusters.

## 4. Feature Engineering
Added derived features:
- `Amount_log` = log(Amount + 1e-3)
- `Amount_square` = Amount²  
These features may capture nonlinear transaction patterns.

## 5. Output Artifacts
- `X_train_res`, `y_train_res` → balanced training set  
- `X_test`, `y_test` → hold-out test set  
- Stored in `KDD/outputs/kdd_transformed.pkl`

  <img width="599" height="467" alt="image" src="https://github.com/user-attachments/assets/1ecd9900-4857-4a96-bc89-6c0cd4a84775" />


## Next Step
Proceed to **KDD Phase 4 – Data Mining**, where we’ll train and evaluate classification models to detect fraudulent transactions.
