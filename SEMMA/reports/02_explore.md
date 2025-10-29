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

## Risks & Limitations
- Some variables (e.g., studytime) are self-reported and may be inaccurate.
- Data may reflect only a single school’s population, limiting generalizability.
