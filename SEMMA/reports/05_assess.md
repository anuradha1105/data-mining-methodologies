# SEMMA Phase 5: Assess

## Objective
The Assess phase evaluates the trained models' performance, robustness, and practical usability for decision-making.

## Evaluation Summary
The Random Forest model performed best on the test data:

<img width="512" height="197" alt="image" src="https://github.com/user-attachments/assets/8fc41316-abcf-4250-b8d1-4f0b1fc0ba3c" />


## Interpretation
- The model demonstrates strong ability to distinguish at-risk students from successful ones.
- Most important predictors:
  1. G2 (2nd period grade)
  2. G1 (1st period grade)
  3. Average prior grades
  4. Absences
  5. Study time

<img width="834" height="473" alt="image" src="https://github.com/user-attachments/assets/ec8a08da-4f84-4779-9369-0df28e94dee6" />

These align with academic intuition — past performance and attendance directly influence risk.

## Confusion Matrix
- **True Positives (TP):** correctly identified at-risk students.  
- **False Negatives (FN):** missed at-risk students (need more focus).  
- **False Positives (FP):** misclassified safe students (acceptable if interventions are low-cost).  

## ROC Curve
<img width="574" height="201" alt="image" src="https://github.com/user-attachments/assets/0ae87005-a6db-4d22-89e6-2368417bbe2d" />
 
The ROC curve indicates strong model discrimination power.

## Validation & Reliability
- Used 80/20 stratified split.
- Tested multiple algorithms for stability.
- Random Forest consistently outperformed simpler models.

## Business/Academic Implications
- Enables early identification of struggling students.
- Provides actionable variables (attendance, prior grades).
- Can be integrated into academic dashboards for real-time monitoring.

## Ethical Considerations
- Predictions should support, not penalize, students.
- Models should be retrained periodically to avoid bias or drift.
- Transparency in model logic is critical when used for student decisions.

## Next Steps
- Deploy model as a predictive API or dashboard.
- Automate retraining each semester.
- Collect more behavioral data for long-term accuracy tracking.
