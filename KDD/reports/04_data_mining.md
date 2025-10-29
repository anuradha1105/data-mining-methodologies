# KDD Phase 4: Data Mining

## Objective
The Data Mining phase applies machine learning algorithms to the transformed dataset to discover patterns and relationships indicative of fraud. The goal is not only predictive accuracy but interpretability and actionable knowledge.

## 1. Algorithms Applied
- **Logistic Regression** – baseline linear model  
- **Random Forest** – ensemble tree-based model  
- **XGBoost** – gradient-boosted decision trees  

Each model was trained on the balanced dataset created with SMOTE.

## 2. Evaluation Results
<img width="586" height="147" alt="image" src="https://github.com/user-attachments/assets/dce7ca81-5261-46c2-a85e-56b5e420c604" />


## 3. Observations
- Random Forest and XGBoost achieve superior results, both exceeding 99.8% ROC-AUC.
- High recall ensures that most fraudulent transactions are detected.
- Logistic Regression underperforms slightly but remains interpretable.

## 4. Visualization Insights
- **Confusion Matrix** confirms minimal false negatives.  
- **ROC Curves** for all models show near-perfect separability (AUC > 0.99).

  <img width="587" height="492" alt="image" src="https://github.com/user-attachments/assets/42275587-0d52-4451-9dc0-efcdbcf00753" />


## 5. Model Selection
The **Random Forest** model was chosen for deployment due to:
- High performance with less overfitting than XGBoost.
- Interpretability through feature importance metrics.

## 6. Stored Artifacts
- `kdd_best_model.pkl` – serialized Random Forest model  
- `results.csv` – model performance metrics  

## Next Step
Proceed to **KDD Phase 5 – Interpretation**, where we’ll analyze the discovered patterns, discuss their real-world meaning, and evaluate the knowledge gained.
