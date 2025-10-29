# KDD Phase 1: Selection

## Objective
The Selection phase identifies and extracts the most relevant data source for knowledge discovery. For this project, we focus on detecting fraudulent credit card transactions.

## Dataset
- **Name:** Credit Card Fraud Detection
- **Source:** Kaggle (mlg-ulb/creditcardfraud)
- **Rows:** [insert df.shape[0]] transactions
- **Columns:** [insert df.shape[1]] features
- **Label Column:** `Class`
  - 0 = legitimate transaction
  - 1 = fraudulent transaction

## Why This Dataset?
- It is a real-world, high-volume dataset (280K+ rows) — realistic for fraud analytics.
- It is highly imbalanced (fraud cases are very rare), which is a classic and important challenge in financial risk modeling.
- It allows us to apply KDD to discover behavioral patterns in fraud, not just train a model.

## Important Attributes
- `V1` ... `V28`: anonymized numeric features derived using PCA from the original transaction data.
- `Amount`: transaction amount in Euros.
- `Time`: time elapsed (in seconds) from the first transaction in the dataset.
- `Class`: fraud indicator (our prediction target).

## Initial Observations
- The dataset is extremely imbalanced. Most rows are class 0 (legit), only a very small % are class 1 (fraud).
- This means we cannot just optimize for accuracy; we must consider precision/recall, F1, ROC-AUC, etc.

## Scope of KDD Project
We will:
1. Select and clean this dataset (Selection + Preprocessing).
2. Transform it (e.g. scaling, resampling).
3. Apply data mining methods (classification + anomaly detection).
4. Interpret results in terms of real anti-fraud operations.
