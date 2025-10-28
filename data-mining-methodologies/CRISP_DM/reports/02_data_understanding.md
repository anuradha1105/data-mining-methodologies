# Phase 2: Data Understanding

## Objective
To explore the dataset, identify data quality issues, detect patterns, and generate hypotheses for modeling.

## Data Overview
- Total rows: (e.g., 6435)
- Total columns: (e.g., 8)
- Target variable: Weekly_Sales
- Feature columns: Store, Dept, Date, IsHoliday, Temperature, Fuel_Price, CPI, Unemployment

## Summary of Findings
- No missing values in most columns except CPI (2%).
- 45 stores × 99 departments.
- Weekly_Sales highly skewed; requires log-scale or normalization.
- Sales spike near holidays.
- Temperature shows mild correlation with Weekly_Sales.

## Risks
- Temporal non-stationarity (sales trend changes over time).
- External factors like promotions not included.
- Potential outliers during holidays.

## Evidence
Include plots:
- Histogram of Weekly_Sales
- Sales vs Date
- Holiday vs Non-Holiday boxplot

---
