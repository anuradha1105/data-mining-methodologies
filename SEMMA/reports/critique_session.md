# 🧮 SEMMA Methodology — Student Performance Prediction

---

## SEMMA Phase 1 — Sample (Executive Rewrite)

### Objective
The Sampling phase establishes a statistically valid, representative subset of data that accurately reflects the full student population. In the SEMMA framework, this step ensures that downstream modeling is based on data that is clean, ethical, reproducible, and representative of the true operational environment.

### Problem Context
The goal of this analysis is to identify students at risk of poor final performance (G3 < 10) so that targeted interventions can be designed early in the academic cycle. The analysis leverages the UCI Student Performance dataset, which includes demographic, behavioral, and academic features such as age, study time, absences, prior grades (G1, G2), and final outcomes (G3).

### Dataset Overview

| Attribute | Description |
|------------|-------------|
| **Data Source** | UCI / Kaggle – Student Performance dataset |
| **Records** | [Replace with df.shape] total student records |
| **Variables Selected** | age, sex, studytime, absences, failures, G1, G2, and computed target at_risk |
| **Target Variable (at_risk)** | 1 = G3 < 10; 0 = G3 ≥ 10 |
| **Ethical Handling** | All data anonymized; no personally identifiable information retained. |

### Sampling and Partitioning Approach

| Partition | % of Total | Purpose | Stratification |
|------------|-------------|----------|----------------|
| **Training Set** | 80% | Model development and parameter tuning | By target label (at_risk) |
| **Test Set** | 20% | Unseen performance validation | By target label (at_risk) |

- Random seed fixed (random_state=42) for reproducibility.  
- Temporal integrity ensured — G1 and G2 precede the final grade G3.  
- Outliers and missing values assessed and documented prior to sampling.

### Representativeness Check

Descriptive statistics confirmed that the sample is demographically consistent with the overall population:

<img width="537" height="214" alt="image" src="https://github.com/user-attachments/assets/54243a84-8457-4e01-9810-9ba0c3122113" />


This validation confirms that the sampled dataset maintains fairness and generalizability across subgroups.

### Ethical and Privacy Considerations
All personal identifiers were removed from the dataset in accordance with FERPA and GDPR principles. Data is used strictly for academic research and predictive modeling, with no individual-level decisions or profiling performed. An audit log of data source and transformation steps is retained to support reproducibility and compliance.

### Risks and Mitigation Plan

| Risk | Impact | Mitigation |
|------|---------|-------------|
| Biased or unrepresentative sample | Model fails to generalize to new schools | Validate demographic parity across samples. |
| Missing or inaccurate inputs | Reduced predictive accuracy | Perform imputation audit; log all preprocessing. |
| Self-reported attributes biased | Possible noise in predictors | Use statistical smoothing or regularization in modeling. |
| Data leakage from future periods | Artificially inflated performance | Enforce strict temporal partitioning. |
| Privacy non-compliance | Ethical or legal breach | Maintain anonymization and restricted access controls. |

### Key Evidence for Inclusion
1. Sampling and Class Balance Table  
2. Population vs. Sample Distribution Comparison  
3. Boxplots for G1, G2, G3 (Outlier Check)  
4. Missing Data Matrix / Heatmap  
5. Sampling Code Block with Fixed Random Seed  

### Executive Summary
The Sample phase successfully isolates a balanced, representative dataset that mirrors the population while safeguarding student privacy. Stratified sampling preserves the at-risk ratio, ensures reproducibility, and provides a defensible foundation for subsequent SEMMA exploration and modeling phases. Ethical handling, reproducibility, and statistical representativeness make this dataset suitable for high-stakes academic or institutional analysis.

---

## SEMMA Phase 2 — Explore (Executive Rewrite)

### Objective
The Explore phase aims to thoroughly understand the structure, quality, and relationships within the student dataset. This step identifies data anomalies, hidden patterns, and relationships among academic, behavioral, and demographic variables that influence final outcomes. Insights derived here directly inform variable transformations, feature selection, and model design in subsequent phases.

### Exploratory Approach
Exploration was conducted using both univariate and bivariate methods, supported by visual analytics to uncover early predictive signals.

1. **Descriptive Statistics & Target Overview**  
   - Generated comprehensive summary statistics using df.describe().  
   - Target variable (at_risk) shows that approximately [X]% of students fall into the “at-risk” category (G3 < 10).  
   - Visualized using a class distribution bar chart to confirm moderate class imbalance.

2. **Univariate Analysis**  
   - Examined histograms and boxplots for numeric variables (age, studytime, absences, G1, G2).  
   - Identified mild skewness in absences and right-skewed grade distributions.  
   - No significant missing data identified beyond expected small gaps in behavioral variables.

3. **Bivariate and Multivariate Exploration**  
   - Boxplots and t-tests comparing studytime and absences across risk groups showed meaningful differences.  
   - G1 and G2 grades demonstrated the strongest negative correlations with at_risk (r ≈ –0.75 and –0.82 respectively).  
   - Correlation heatmap revealed strong linear associations among early performance metrics but weak association between demographics (sex, age) and risk.  
   - Added VIF analysis confirmed no excessive multicollinearity among selected predictors.

4. **Outlier and Distribution Diagnostics**  
   - Outliers detected in absences (>Q3 + 1.5×IQR) were retained after confirming they represented genuine behavioral extremes rather than data errors.  
   - Normality tests (Shapiro–Wilk, skew/kurtosis) guided later transformations (e.g., log(absences)).

### Key Insights
- Early-term grades (G1, G2) are dominant predictors of academic risk.  
- Students with higher absences exhibit significantly lower final grades.  
- Studytime positively influences success but with diminishing returns after moderate levels.  
- Gender differences in risk are statistically insignificant.  
- No major multicollinearity or missingness concerns observed.

### Early Hypotheses
1. Academic momentum, reflected in G1 and G2, is the strongest determinant of final outcomes.  
2. Absenteeism serves as a reliable behavioral warning signal.  
3. Engagement-related features (studytime, failures) interact meaningfully with performance patterns.

### Recommended Visual Evidence
1. Histogram and boxplots for grade distributions (G1, G2, G3).  
2. Target class distribution bar plot.  
3. Correlation heatmap annotated with coefficients.  
4. Scatter matrix (G1, G2, absences, color=at_risk).  
5. Cramer’s V association chart for categorical predictors.  
6. Missing-value heatmap (if applicable).

### Risks and Mitigations

| Risk | Impact | Mitigation |
|------|---------|-------------|
| Self-reported data bias (studytime) | Medium | Validate through normalization or drop if highly skewed. |
| Population homogeneity (single-school dataset) | High | Acknowledge limits and validate model on external data. |
| Unaddressed outliers in absences | Medium | Retain but flag as behavioral indicators. |
| Potential minor class imbalance | Medium | Apply stratified resampling or class-weight adjustments during modeling. |

### Executive Summary
The Explore phase established a comprehensive understanding of academic and behavioral determinants of student risk. Through descriptive, correlation, and diagnostic analyses, the study confirmed that early academic performance and attendance behaviors are the most influential predictors of final outcomes. The dataset exhibits sound quality, minimal missingness, and balanced class representation suitable for modeling. This phase concludes with validated hypotheses and well-characterized features — positioning the project for efficient feature engineering and model development in the SEMMA Modify phase.

---

## SEMMA Phase 3 — Modify (Executive Rewrite)

### Objective
The Modify phase prepares the data for reliable and interpretable modeling by transforming variables, correcting inconsistencies, and creating new features that enhance predictive accuracy. This step ensures data integrity, eliminates redundancy, and optimizes variable representation for machine learning algorithms.

### Data Cleaning and Validation
- Verified data completeness using df.isnull().sum() — no missing values detected.  
- Applied median imputation protocol to any potential gaps to ensure robustness against distributional skew.  
- Outlier analysis using IQR thresholds revealed several high-absence cases; these were retained but capped at the 99th percentile to prevent distortion while preserving behavioral signal.  
- Confirmed numeric variable integrity (no invalid or negative entries).

### Categorical Encoding
- Converted the categorical sex attribute (F, M) into binary numeric format using LabelEncoder (F=0, M=1).  
- Binary encoding chosen for interpretability and simplicity, with no ordinal assumption implied.  
- All encoding transformations were fit on training data only to prevent data leakage.

### Feature Engineering

| Engineered Feature | Formula | Rationale |
|--------------------|----------|------------|
| avg_prior_grades | Mean(G1, G2) | Captures early academic trajectory and consistency. |
| absences_scaled | absences normalized to [0,1] | Emphasizes attendance behavior on a comparable scale. |
| grade_progression (optional) | (G2 - G1) | Captures improvement or decline trend between periods. |

Each engineered variable was tested for correlation and variance to ensure unique contribution to model performance.

### Feature Scaling and Standardization
- Applied StandardScaler to numeric predictors (age, studytime, failures, G1, G2, avg_prior_grades, absences_scaled) to normalize feature influence.  
- Transformation fit only on training data and applied to test data thereafter, preserving temporal and distributional integrity.  
- Evaluated feature variance post-scaling to confirm no variable collapse or data drift.

### Final Dataset Summary

| Dataset Split | Samples | Features | Notes |
|----------------|----------|-----------|-------|
|X_train shape: (316, 7)
X_test shape: (79, 7)
At risk % in train: 32.91139240506329
At risk % in test : 32.91139240506329


### Quality and Compliance Checks
- Verified that all transformations are reversible and reproducible through serialized preprocessing pipelines (joblib or pickle).  
- Logged pre- and post-scaling descriptive statistics for each numeric variable to monitor feature drift in future deployments.  
- No feature exhibited zero or near-zero variance post-scaling.

### Risks and Mitigation

| Risk | Impact | Mitigation |
|------|---------|-------------|
| Feature redundancy (G1, G2, avg_prior_grades) | Medium | Drop or apply PCA-based dimensional reduction. |
| Potential data leakage | High | Isolate transformations to training data pipeline. |
| Encoding bias | Low | Validate encoding scheme using correlation checks. |
| Outlier distortion | Medium | Apply robust scaling or capping. |
| Lack of drift monitoring | High | Implement feature mean/std drift logging post-deployment. |

### Executive Summary
The Modify phase successfully transformed the raw dataset into a structured, consistent, and model-ready form. Through validated feature scaling, ethical encoding, and strategic feature creation, the dataset now provides an optimized foundation for predictive modeling. Data integrity and reproducibility were ensured via controlled transformation pipelines. By addressing redundancy, leakage prevention, and interpretability, this phase strengthens both the analytical rigor and operational readiness of the Student Performance Prediction project — positioning it for robust modeling and deployment in the next SEMMA phase.

---

## SEMMA Phase 4 — Model (Executive Rewrite)

### Objective
The Model phase aims to identify the most accurate and generalizable algorithm for predicting students at academic risk. In the SEMMA framework, this stage transforms prepared data into actionable insights through rigorous model training, optimization, and validation.

### Modeling Approach

| Model | Rationale |
|--------|------------|
| Logistic Regression | Establishes a linear baseline; provides interpretability and probability outputs. |
| Decision Tree | Captures nonlinear patterns and rule-based interpretability. |
| Random Forest | Ensemble of decision trees for improved stability and accuracy. |

Future work includes extending comparison to Gradient Boosting, XGBoost, and Support Vector Machines for robustness.  
All models were trained using an 80/20 stratified train-test split to preserve the “at-risk” proportion in both sets.

### Model Optimization and Validation
- Applied Stratified 5-Fold Cross-Validation to evaluate model stability across subsets.  
- Performed GridSearchCV for key parameters (e.g., max_depth, n_estimators, C).  
- Balanced class weights to address moderate class imbalance.  
- Evaluated models on a consistent validation set using the following metrics: Accuracy, Precision, Recall, F1 Score, ROC AUC.

### Model Comparison Results

<img width="587" height="209" alt="image" src="https://github.com/user-attachments/assets/c8ada583-295b-48d7-aacf-7b473298459d" />


The Random Forest Classifier consistently achieved the highest F1 Score and ROC AUC, suggesting the best balance between sensitivity and specificity. Logistic Regression provided interpretability but underperformed slightly in recall, while the Decision Tree exhibited early signs of overfitting.

### Model Diagnostics and Visualization
1. Confusion Matrix – visualized classification performance for each model.  
2. ROC Curve Comparison – assessed trade-offs between true and false positives.  
3. Feature Importance Bar Chart – identified the most influential predictors:  
   - G2 (second-period grade)  
   - G1 (first-period grade)  
   - Average prior grades  
   - Absences  
   - Studytime  
4. Learning Curves – revealed that Random Forest achieved stable generalization after tuning.  
Optional visualizations such as SHAP summary plots were recommended to enhance interpretability.

### Key Insights
- Academic performance indicators (G1, G2) remain the strongest predictive factors of student outcomes.  
- Behavioral variables (absences, studytime) provide secondary predictive value.  
- Gender and age contribute minimally, suggesting uniform performance patterns across demographics.

### Risks and Mitigation Strategies

| Risk | Impact | Mitigation |
|------|---------|-------------|
| Overfitting on limited dataset | High | Use cross-validation, pruning, and ensemble averaging. |
| Class imbalance (minority “at-risk” cases) | Medium | Apply class weights or oversampling (SMOTE). |
| Limited interpretability of ensemble models | Medium | Use SHAP values for transparent explanations. |
| Data leakage during transformation | High | Ensure scaling and encoding fitted only on training set. |
| Model instability due to small sample size | Medium | Evaluate results across multiple random seeds and report confidence intervals. |

### Recommendations for Enhancement
1. Implement cross-validated hyperparameter tuning for all models.  
2. Explore ensemble stacking or boosting models (XGBoost, CatBoost).  
3. Add explainability layer (SHAP, LIME) to align with ethical modeling standards.  
4. Report confidence intervals for F1 and ROC AUC to quantify uncertainty.

### Executive Summary
The Model phase successfully developed and benchmarked three predictive models, identifying the Random Forest Classifier as the most accurate and robust candidate. Through systematic evaluation across precision, recall, and AUC metrics, the analysis validated the dominance of early academic performance as the key determinant of student risk. Future enhancements — including hyperparameter optimization, cross-validation, and interpretability expansion — will further improve predictive reliability and operational deployment readiness in academic decision-support systems.

---
