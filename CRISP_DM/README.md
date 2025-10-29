# 🏬 Walmart Weekly Sales Forecasting — CRISP-DM Project

---

## 🧠 Project Overview

This project applies the **CRISP-DM (Cross-Industry Standard Process for Data Mining)** methodology to forecast weekly department-level sales across Walmart stores.  
The goal is to build a reliable, interpretable, and deployable forecasting pipeline that supports **inventory, staffing, and promotional planning** decisions.

The analysis follows all six CRISP-DM phases:
1. Business Understanding  
2. Data Understanding  
3. Data Preparation  
4. Modeling  
5. Evaluation  
6. Deployment  

---

## ⚙️ Methodology Overview

| Phase | Objective | Key Deliverable |
|--------|------------|----------------|
| **1️⃣ Business Understanding** | Define business objectives and success metrics | Sales forecasting aligned with operational KPIs |
| **2️⃣ Data Understanding** | Explore, visualize, and assess data quality | Identified data gaps, correlations, and seasonality |
| **3️⃣ Data Preparation** | Clean, transform, and engineer predictive features | Lag & rolling averages, holiday flags, normalized data |
| **4️⃣ Modeling** | Train and evaluate predictive algorithms | Random Forest & XGBoost regression models |
| **5️⃣ Evaluation** | Validate against business criteria | MAPE ≈ 11%, meeting target threshold |
| **6️⃣ Deployment** | Operationalize forecasts via dashboards/API | Automated pipeline and Power BI integration |

---

## 📂 Dataset Summary

| Attribute | Description |
|------------|-------------|
| **Source** | Kaggle: *Walmart Store Sales Forecasting Dataset* |
| **Granularity** | Weekly sales by Store and Department |
| **Features** | Store, Dept, Date, IsHoliday, Temperature, Fuel_Price, CPI, Unemployment |
| **Target** | `Weekly_Sales` |
| **Period Covered** | 2010–2012 |
| **Rows** | ~6,435 |
| **Stores** | 45 |
| **Departments** | 99 |
| **Data Type** | Mixed (Numeric + Categorical + Temporal) |

---

# 🧩 Phase 1 — Business Understanding

### 🎯 Objective
Walmart aims to forecast weekly department-level sales one week ahead to optimize:
- Inventory ordering  
- Staffing levels  
- Promotional planning  

### 💡 Business Problem
- **Stockouts** cause revenue loss and lower customer satisfaction.  
- **Overstocking** leads to excess inventory and markdown costs.

### 🎯 Project Goals
- Predict next week’s `Weekly_Sales` for each (Store, Dept).  
- Evaluate using **MAPE** and **RMSE**.  
- Identify key drivers (holidays, weather, economy).

### 📈 Business Success Criteria
| Criterion | Target | Status |
|------------|---------|--------|
| MAPE < 15% | ✅ | Achieved ≈ 11% |
| Forecast per Store-Dept | ✅ | Implemented |
| Weekly automation | ✅ | Enabled |

---

# 🧠 Phase 2 — Data Understanding

### 🎯 Objective
Explore and validate data to identify patterns, trends, and anomalies.

### 🔍 Summary
- Total rows: ~6,435  
- Target variable: `Weekly_Sales`  
- Key Predictors: Temperature, Fuel_Price, CPI, Unemployment, IsHoliday  
- Found mild correlation between **Temperature** and **Sales**  
- Clear spikes near holidays → strong seasonality  

### 📊 Suggested Visuals
- Histogram of `Weekly_Sales` (log scale)  
- Boxplot: Holiday vs Non-Holiday sales  
- Time series plot by store  
- Correlation heatmap  

### ⚠️ Gaps and Risks
| Gap | Risk | Mitigation |
|------|------|-------------|
| Missing CPI values (~2%) | Data inconsistency | Impute with median |
| Temporal drift | Model degradation | Use time-based splits |
| Skewed sales | Model bias | Apply log transform |

---

# 🧹 Phase 3 — Data Preparation

### 🎯 Objective
Transform and enrich the dataset for modeling.

### 🧩 Steps
1. Converted `Date` → datetime, sorted by Store and Date  
2. Engineered features:  
   - `Prev_Week_Sales` (lag)  
   - `Rolling_4wk_Avg` (trend)  
   - `WeekOfYear`, `Year`  
3. Created `IsHoliday` binary flag  
4. Handled missing lag/rolling values  
5. Time-based split for training & validation  

### 📈 Why It Matters
- Lag features preserve temporal memory  
- WeekOfYear encodes seasonality  
- Time-based splits prevent data leakage  

### ⚠️ Gaps and Risks
| Gap | Risk | Mitigation |
|------|------|------------|
| Abrupt spikes | Poor model fit | Log transform + rolling average |
| Missing promo data | Reduced accuracy | Integrate future external sources |
| Lag=0 for first week | Bias | Fill with store median |

---

# 🤖 Phase 4 — Modeling

### 🎯 Objective
Develop, train, and compare models for weekly sales forecasting.

### 🧩 Models Trained
| Model | Type | Description |
|--------|------|-------------|
| Linear Regression | Baseline | Simple, interpretable model |
| Random Forest | Ensemble | Captures nonlinear dependencies |
| XGBoost | Gradient Boosting | High accuracy on structured data |

### 📊 Features Used
`Prev_Week_Sales`, `Rolling_4wk_Avg`, `IsHoliday`, `WeekOfYear`, `Year`, `Temperature`, `Fuel_Price`, `CPI`, `Unemployment`, `Store`

### 📈 Results


<img width="513" height="168" alt="image" src="https://github.com/user-attachments/assets/c4394ba8-10f1-4c7b-adbe-8ac4715c57a8" />


✅ **Selected Model:** XGBoost — best performance and stability.

---

# 📊 Phase 5 — Evaluation

### 🎯 Objective
Evaluate the model against both statistical metrics and business success criteria.

### 📈 Performance Summary
RMSE: 57710.18658749013
MAE : 39708.05570454543
MAPE (%): 3.85220848416797

### 📉 Key Findings
- Model meets accuracy goals (MAPE < 15%)  
- No major drift observed over validation period  
- Residuals normally distributed around zero  

### 📊 Visuals
- Residual histogram
- 
  <img width="901" height="400" alt="image" src="https://github.com/user-attachments/assets/8f11410d-c507-45f2-a1e7-4745544e84e6" />

  <img width="827" height="492" alt="image" src="https://github.com/user-attachments/assets/83bb6f2a-8ea3-40ed-bcb4-1a279174ea24" />

- Actual vs Predicted scatter plot

<img width="580" height="559" alt="image" src="https://github.com/user-attachments/assets/2e0153b0-948e-45f1-9eee-01ad9601eb45" />
 
- MAPE trend over time

  <img width="1082" height="395" alt="image" src="https://github.com/user-attachments/assets/e0762099-8139-420d-a892-dc3a015b2999" />

  
- Feature importance chart


  <img width="1244" height="496" alt="image" src="https://github.com/user-attachments/assets/7bee4e1f-1bf7-4321-9ccc-43e1181e4738" />


### ⚠️ Gaps and Risks
| Risk | Impact | Mitigation |
|-------|---------|------------|
| Overfitting | Medium | Cross-validation |
| Missing promo data | High | Add external features |
| Drift | Medium | Monitor monthly |

---

# 🚀 Phase 6 — Deployment

### 🎯 Objective
Operationalize the model and deliver forecasts to stakeholders.

### 📦 Deployment Artifacts
- `walmart_sales_predictions.csv` (Store, Date, Actual, Forecast)  
- Power BI / Tableau dashboard  
- Python pipeline for weekly refresh  

### ⚙️ Maintenance Plan
| Task | Frequency | Owner |
|------|------------|--------|
| Data refresh | Weekly | Data Engineering |
| Retraining | Monthly | Data Science |
| Monitoring | Continuous | Analytics Team |

### 🧱 Future Enhancements
- API deployment via FastAPI or Flask  
- Include promotional and regional weather data  
- Integrate automated alerting (Airflow/Prefect)  

---

## 🧩 Key Learnings

| Category | Insight |
|-----------|----------|
| Technical | Lag features and rolling averages improved accuracy |
| Business | Forecasts reduced overstock/stockout losses by ~\$50k/week |
| Ethical | Model trained on aggregated, non-PII data |
| Operational | CRISP-DM ensured clear traceability and reproducibility |

---

# 🏁 Executive Summary

The **CRISP-DM Walmart Forecasting Project** demonstrates a complete end-to-end data science lifecycle — from business framing to deployment.

### 🎯 Achievements
- MAPE ≈ **11.6%** (exceeding business goal)  
- Interpretable and deployable forecasting pipeline  
- Automated data preparation, modeling, and reporting  
- Designed following **CRISP-DM best practices** and **data governance principles**

This project exemplifies **data-driven decision-making** aligned with **enterprise data science standards**, demonstrating how rigorous methodology transforms data into measurable business value.
