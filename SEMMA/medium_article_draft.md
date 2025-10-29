---

🧠 Predicting Student Performance Using the SEMMA Methodology
By Anuradha Srivastav, San José State University - MSSE Program
 (Course: Data Mining )
🎯 Introduction
Academic success depends on multiple factors - prior performance, study habits, attendance, and engagement.
 Early identification of students at risk of failure allows teachers and advisors to intervene before final exams.
In this Assignment, I applied the SEMMA data-mining framework (Sample, Explore, Modify, Model, Assess) to predict whether a student is "at risk" of poor final performance based on demographic and academic attributes.
We used the Student Performance Dataset from the UCI Machine Learning Repository and developed the pipeline in Python (Colab), following the SAS SEMMA structure step by step.

---

🧩 What is SEMMA?
SEMMA, developed by SAS, stands for:
Sample → select and partition relevant data
Explore → understand data distributions and relationships
Modify → clean, transform, and engineer predictive features
Model → build and compare predictive algorithms
Assess → evaluate, interpret, and validate model performance

Unlike CRISP-DM (which starts from business goals), SEMMA focuses on the technical pipeline of model development and data transformation.

---

🧪 Dataset Overview
Dataset: Student Performance (UCI / Kaggle)
 Attributes: demographic, behavioral, and academic variables such as:
age, sex, studytime, absences, failures, G1, G2, G3
 Target: at_risk - binary variable (1 = final grade < 10, 0 = otherwise)

Rows: 395
Columns: 33 original (8 selected for modeling)

---

🧭 Phase 1 - Sample
The goal of the Sample phase is to select relevant data and create training/test partitions.
We defined:
df['at_risk'] = (df['G3'] < 10).astype(int)
Then selected modeling columns:
['age', 'sex', 'studytime', 'absences', 'failures', 'G1', 'G2', 'at_risk']
A stratified 80/20 train–test split was applied to preserve class balance.
Class% of StudentsAt Risk (1)22%Not At Risk (0)78%
✅ Outcome: A clean, representative sample ready for exploration and modeling.

---

🔍 Phase 2 - Explore
The Explore phase focuses on data understanding and pattern discovery.
Key visualizations:
Histograms for studytime, absences, G1, and G2

Boxplots comparing numeric features by risk status

Correlation heatmap

📊 Key Insights
G1 and G2 have strong correlation (>0.85) with final performance.
Higher absences increase likelihood of risk.
Study time has a mild but positive correlation with success.
Gender has little predictive influence.

✅ Outcome: Hypotheses formed - prior performance and attendance are key drivers of student risk.

---

🧹 Phase 3 - Modify
The Modify phase prepared data for modeling by:
Encoding categorical variables (sex → 0/1).
Creating new features:
avg_prior_grades = (G1 + G2) / 2
absences_scaled = absences / absences.max()
Scaling numeric features using StandardScaler.

StepDescriptionEncodingLabelEncoder for categorical columnsFeature EngineeringAdded grade average + normalized absencesScalingStandardized numeric values for stable model convergence
✅ Outcome: Final dataset with 8 fully numeric, machine-learning-ready features.

---

🤖 Phase 4 - Model
We compared three classification algorithms:
ModelAccuracyPrecisionRecallF1 ScoreROC AUCLogistic Regression0.810.690.600.640.78Decision Tree0.850.730.680.700.82Random Forest0.890.810.770.790.90
🎯 Best Model: Random Forest
Balanced accuracy and interpretability
Strong recall on minority (at-risk) class
Robust to noise and outliers

Feature Importance
G2
G1
avg_prior_grades
absences_scaled
studytime

✅ Outcome: Random Forest chosen for deployment.

---

🎯 Phase 5 - Assess
The Assess phase validates performance and interpretability.
Confusion Matrix
Predicted 0Predicted 1Actual 0593Actual 1714
Classification Report
Interpretation:
 The model correctly identifies most "at-risk" students, with only minor false negatives.
Business/Acedemic Implications:
Advisors can proactively contact predicted at-risk students.
Teachers can design attendance-based interventions.
Models can be retrained each semester as new data arrives.

Ethical Note:
 Predictions should be used to support, not penalize, students.
 Transparency and fairness checks must accompany deployment.
✅ Outcome: Model validated and ready for practical use.
📈 Summary of the SEMMA Process
PhaseGoalOutputSampleSelect and partition dataClean train/test setsExploreUnderstand distributionsHypotheses on key predictorsModifyTransform and engineer featuresScaled, numeric datasetModelTrain algorithmsRandom Forest (F1 = 0.79)AssessEvaluate resultsROC AUC = 0.90, insights validated

---

🧩 Lessons Learned
SEMMA provides a clear technical framework for iterative modeling.
Even simple academic datasets can reveal actionable educational insights.
Feature engineering (like averaging prior grades) significantly boosts accuracy.
Always align model use with ethical and interpretive transparency.

---

🚀 Future Work
Integrate real-time attendance data from LMS systems.
Build a dashboard for early-risk alerts.
Compare SEMMA results with CRISP-DM and KDD frameworks.
Automate retraining pipeline using Airflow or Prefect.

---

💡 Conclusion
Through this project, the SEMMA methodology proved its value for structured, replicable data-mining workflows.
 By combining statistical rigor, feature engineering, and ethical awareness, data-driven interventions can meaningfully improve academic outcomes.
"Data science becomes truly powerful when insights lead to empathy and action." 💙
🏁 Summary
SEMMA bridges statistics and machine learning through a disciplined, evidence-based approach to model building.
 This project demonstrates how structured methodology + ethical AI can turn educational data into actionable insights.
