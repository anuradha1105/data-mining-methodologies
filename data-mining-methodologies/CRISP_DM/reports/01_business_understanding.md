# Phase 1: Business Understanding

## Objective
Walmart wants to predict **weekly department-level sales** across its stores.  
By forecasting demand, managers can optimize:
- inventory ordering
- staffing levels
- promotional planning

## Business Problem
Stockouts lead to lost sales and unsatisfied customers.  
Overstocking leads to excess storage and discount losses.  
The goal is to **forecast Weekly_Sales** for each store and department one week in advance.

## Project Goals
- Predict next week's Weekly_Sales using historical data.
- Evaluate models by **MAPE (Mean Absolute Percentage Error)** and **RMSE**.
- Identify key drivers (holidays, temperature, fuel price, etc.).
- Provide a deployable pipeline for weekly updates.

## Business Success Criteria
- Achieve MAPE < 15%.
- Provide interpretable forecasts per store-department.
- Enable automated weekly updates.

## Constraints
- Seasonal patterns and holiday spikes.
- Missing or noisy data in external factors (CPI, Unemployment).
- Limited historical range.

## Stakeholders
- **Store Managers:** daily operations
- **Regional Finance Team:** budget planning
- **Supply Chain Team:** ordering and logistics

## ROI Impact
A 2% improvement in forecast accuracy could reduce weekly overstock and stockout losses by an estimated \$50,000 across all stores.

---
