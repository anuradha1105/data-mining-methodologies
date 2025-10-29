# SEMMA Phase 2: Explore

## Goal of the Phase
The Explore phase focuses on understanding the data distribution, identifying outliers, relationships between predictors, and finding early signals about what drives student performance.

## Exploratory Steps
1. Generated summary statistics using `df.describe()`.
2. Visualized target variable (`at_risk`) distribution:
   - Approximately **[X]% of students** are classified as "at risk".
3. Examined univariate distributions for `age`, `studytime`, `absences`, `G1`, and `G2`.
4. Conducted bivariate analysis to explore how predictors vary across the target:
   - Boxplots of studytime vs at_risk.
   - Boxplots of absences vs at_risk.
   - Countplot of gender (sex) vs at_risk.
5. Computed feature correlation matrix to understand linear relationships.

## Key Insights
- **G1** and **G2** show strong negative correlation with `at_risk`.
- Students with higher absences tend to have lower final grades.
- Studytime has a positive but modest impact on success.
- Gender does not appear to influence risk substantially.

## Early Hypotheses
- Academic performance in early terms (`G1`, `G2`) is a powerful predictor of risk.
- Attendance is a behavioral risk indicator.
- Combining early grades and absences will likely yield strong model performance.

## Visual Evidence
- Figure 1: Histogram of numeric features.
- Figure 2: Boxplots of absences/studytime vs at_risk.
- Figure 3: Correlation heatmap.
  
<img width="867" height="507" alt="image" src="https://github.com/user-attachments/assets/c170b46f-0915-4bdc-b6ee-f62f97cd1002" />

<img width="656" height="455" alt="image" src="https://github.com/user-attachments/assets/df63afa8-54bd-4c26-b7af-bfbb51eca239" />

<img width="882" height="578" alt="image" src="https://github.com/user-attachments/assets/9df5665c-49a3-4d97-9387-cfe61687bf2d" />

<img width="612" height="454" alt="image" src="https://github.com/user-attachments/assets/a6f34756-20d8-4cbc-b06a-9b110d36c860" />

<img width="723" height="537" alt="image" src="https://github.com/user-attachments/assets/89ba17a9-4604-41bb-a45d-d52a1c31d559" />

<img width="511" height="199" alt="image" src="https://github.com/user-attachments/assets/b9da6cd3-b3b5-42af-940d-3b3ce23cab80" />






## Risks & Limitations
- Some variables (e.g., studytime) are self-reported and may be inaccurate.
- Data may reflect only a single school’s population, limiting generalizability.
