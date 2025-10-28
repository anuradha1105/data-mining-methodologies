# Phase 3: Data Preparation

## Goal
Prepare the Walmart weekly sales data so it is clean, consistent, and feature-rich for modeling.

## Steps Performed
1. Converted `Date` to datetime and sorted records by Store and Date.
2. Engineered time-based features:
   - `WeekOfYear`
   - `Year`
3. Added business features:
   - `Prev_Week_Sales`: last week's sales per Store
   - `Rolling_4wk_Avg`: rolling 4-week average sales per Store
   - `IsHoliday`: binary flag for holiday periods (where available)
4. Handled missing values:
   - Filled missing `Prev_Week_Sales` with 0 for the first observed week of each store
   - Filled missing `Rolling_4wk_Avg` with median
5. Performed a **time-based split**:
   - Training data = earlier dates
   - Validation data = later dates
   - This simulates real forecasting instead of random shuffling
6. (If applied) Created `Weekly_Sales_Log` to stabilize extreme spikes.

## Why This Matters
- Lag and rolling-average features give the model memory of recent performance.
- WeekOfYear captures seasonality and holiday effects.
- Time-based split prevents data leakage from the future into the past.

## Risks / Notes
- Abrupt spikes (e.g. Black Friday) may still be hard to model.
- External promo data is not included, which limits accuracy.
- Filling missing lag values with 0 may under-estimate first-week sales in new stores.

---
