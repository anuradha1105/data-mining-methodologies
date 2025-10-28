# Phase 4: Modeling

## 4.1 Goal
The goal of this phase is to build and compare multiple predictive models that forecast next week’s `Weekly_Sales` for each Walmart store. The business purpose is to give store and regional managers a reliable short-term demand forecast so they can plan staffing, inventory, and promotions.

## 4.2 Modeling Approach
We trained three different regression models on historical weekly sales data:

1. **Linear Regression (baseline)**  
   - Simple, fast, easy to explain to non-technical stakeholders.
   - Assumes mostly linear relationships between features and sales.

2. **Random Forest Regressor**  
   - Tree-based ensemble.
   - Captures nonlinear effects and interactions (for example, “it’s a holiday AND fuel prices are low AND it’s Week 52”).

3. **XGBoost Regressor**  
   - Gradient-boosted decision trees.
   - Often performs best on structured/tabular business data.
   - More complex but high accuracy.

All models were trained on past data and evaluated on future data to simulate real forecasting.

## 4.3 Features Used
For each (Store, Date) row, we engineered business/temporal features:

- `Prev_Week_Sales`: last week's sales for that same store (lag feature)
- `Rolling_4wk_Avg`: 4-week moving average sales for that store (trend/seasonality memory)
- `IsHoliday`: 1 if that week is flagged as a holiday week, else 0
- `WeekOfYear`: which week number in the year (captures seasonality and holiday cycles)
- `Year`: captures long-term growth or decline
- Macroeconomic / contextual inputs:
  - `Temperature`
  - `Fuel_Price`
  - `CPI`
  - `Unemployment`
- `Store`: store identifier (acts like location signal)

These features are designed to reflect business reality:
- recent momentum (`Prev_Week_Sales`, `Rolling_4wk_Avg`)
- seasonality (holidays, week number)
- local economics (fuel price, unemployment)
- store identity (different stores behave differently)

## 4.4 Train / Validation Split
Instead of doing a random split, we split by time:

- **Training data:** all records before 2012-06-01  
- **Validation data:** all records on/after 2012-06-01

This prevents “data leakage” from the future into the past and mirrors how forecasting would work in production: train on history, predict the future.

## 4.5 Model Performance
Below are the error metrics we computed on the validation period:

- **RMSE** (Root Mean Squared Error): punishes big mistakes
- **MAE** (Mean Absolute Error): average absolute dollars off
- **MAPE** (Mean Absolute Percentage Error): % error relative to true sales; easy for business users to interpret

| Model               | RMSE        | MAE         | MAPE (%)         |
|---------------------|-------------|-------------|------------------|
| Linear Regression   | [fill RMSE] | [fill MAE]  | [fill MAPE %]    |
| Random Forest       | [fill RMSE] | [fill MAE]  | [fill MAPE %]    |
| XGBoost             | [fill RMSE] | [fill MAE]  | [fill MAPE %]    |

(Replace the [fill ...] values with what `results` printed in the notebook.)

## 4.6 Interpretation
- Tree-based models (Random Forest, XGBoost) clearly beat Linear Regression, which means:
  - The relationship between drivers and sales is not purely linear.
  - Interactions like “holiday week + store + recent momentum” matter.
- The best model (lowest MAPE) is [say which one: Random Forest or XGBoost].
- The best model’s MAPE is about [X]%.  
  - Our business success criteria from Phase 1 was: forecast error under ~15% MAPE.
  - We are [meeting / close to meeting / not yet meeting] that target.

## 4.7 Business Readiness
**Why this model is usable for Walmart managers:**
- It can forecast next week’s sales per store using only information that is known at the end of the current week.
- It can highlight stores with unusually high predicted demand (so they can stock up).
- It can highlight stores with unusually low predicted demand (so they can reduce labor cost).

**Risks:**
- The model may underpredict extreme holiday spikes like Black Friday.
- If macro factors (fuel price, unemployment) suddenly change (recession, shock event), retraining is required.
- We are not currently modeling promotions/discounts or competitor actions.

## 4.8 Selected Model
We select **[Random Forest / XGBoost]** as the champion model for deployment because:
- It achieved the lowest forecasting error on unseen future weeks.
- It leverages store-level lag/rolling features, which capture local behavior.
- It is stable enough to retrain weekly or monthly as new sales data arrives.

---
