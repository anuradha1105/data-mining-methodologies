# SEMMA Phase 3: Modify

## Objective
The Modify phase focuses on improving data quality and transforming variables to create a clean and predictive modeling dataset.

## Data Cleaning
- Checked for missing values using `df.isnull().sum()` — none found.
- Filled any potential missing values with median values for robustness.
- Ensured all numeric fields are valid and free from outliers.

## Categorical Encoding
- Converted `sex` variable from text ('F', 'M') to numeric using LabelEncoder:
  - F → 0, M → 1
- This ensures compatibility with scikit-learn models.

## Feature Engineering
- Created new derived variable `avg_prior_grades` = mean(G1, G2)  
  Rationale: early academic performance is predictive of final outcome.
- Added `absences_scaled` = absences normalized to [0,1] range.  
  Rationale: high absences often correspond to lower performance.

## Feature Scaling
- Standardized numeric features (`age`, `studytime`, `absences_scaled`, `failures`, `G1`, `G2`, `avg_prior_grades`) using StandardScaler to ensure all have mean 0 and variance 1.
- Scaling helps algorithms like Logistic Regression converge faster and perform better.

## Final Data Shape
- Training samples: [X_train.shape[0]]
- Test samples: [X_test.shape[0]]
- Total features after modification: [X_train.shape[1]]

## Why This Step Matters
This step ensures the data is:
- Machine-learning ready.
- Consistent, numeric, and free from missing data.
- Augmented with engineered features that improve predictive power.

## Next Step
Proceed to the **Model** phase, where different algorithms (Logistic Regression, Decision Tree, Random Forest) will be trained and evaluated on this dataset.
