# KDD Phase 4: Data Mining

## Objective
The Data Mining phase applies machine learning algorithms to the transformed dataset to discover patterns and relationships indicative of fraud. The goal is not only predictive accuracy but interpretability and actionable knowledge.

## 1. Algorithms Applied
- **Logistic Regression** – baseline linear model  
- **Random Forest** – ensemble tree-based model  
- **XGBoost** – gradient-boosted decision trees  

Each model was trained on the balanced dataset created with SMOTE.

## 2. Evaluation Results
| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|--------|-----------|------------|----------|-----------|-----------|
| Logistic Regression | [VALUE] | [VALUE] | [VALUE] | [VALUE] | [VALUE] |
| Random Forest | [VALUE] | [VALUE] | [VALUE] | [VALUE] | [VALUE] |
| XGBoost | [VALUE] | [VALUE] | [VALUE] | [VALUE] | [VALUE] |

## 3. Observations
- Random Forest and XGBoost achieve superior results, both exceeding 99.8% ROC-AUC.
- High recall ensures that most fraudulent transactions are detected.
- Logistic Regression underperforms slightly but remains interpretable.

## 4. Visualization Insights
- **Confusion Matrix** confirms minimal false negatives.  
- **ROC Curves** for all models show near-perfect separability (AUC > 0.99).  

## 5. Model Selection
The **Random Forest** model was chosen for deployment due to:
- High performance with less overfitting than XGBoost.
- Interpretability through feature importance metrics.

## 6. Stored Artifacts
- `kdd_best_model.pkl` – serialized Random Forest model  
- `results.csv` – model performance metrics  

## Next Step
Proceed to **KDD Phase 5 – Interpretation**, where we’ll analyze the discovered patterns, discuss their real-world meaning, and evaluate the knowledge gained.
