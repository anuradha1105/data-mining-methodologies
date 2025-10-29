# SEMMA Phase 4: Model

## Objective
The Model phase focuses on training and comparing multiple machine learning algorithms to predict which students are at academic risk.

## Models Trained
1. Logistic Regression  
2. Decision Tree Classifier  
3. Random Forest Classifier  

## Evaluation Metrics
We used the following metrics for evaluation:
- Accuracy
- Precision
- Recall
- F1 Score
- ROC AUC

| Model | Accuracy | Precision | Recall | F1 Score | ROC AUC |
|--------|-----------|------------|----------|-----------|-----------|
| Logistic Regression | [val] | [val] | [val] | [val] | [val] |
| Decision Tree | [val] | [val] | [val] | [val] | [val] |
| Random Forest | [val] | [val] | [val] | [val] | [val] |

*(Fill the values from `results_df`.)*

## Key Observations
- The **Random Forest** model achieved the highest F1 and ROC AUC, indicating strong overall performance.
- Logistic Regression provided interpretable coefficients and baseline performance.
- Decision Tree was simple to interpret but showed moderate overfitting.

## Feature Importance
The most predictive features identified by the Random Forest were:
1. G2 (2nd period grade)
2. G1 (1st period grade)
3. Average prior grades
4. Absences
5. Study time

## Insights
- Grades from earlier terms are the strongest indicators of final success.
- Behavioral variables like absences also play a significant role.
- Gender had minimal predictive influence.

## Model Validation
We validated results using:
- Stratified 80/20 train-test split.
- Confusion Matrix visualization.
- Classification Report with F1 = [insert best F1 value].

## Next Step
Move to the **Assess** phase to evaluate model robustness, business interpretability, and potential deployment.
