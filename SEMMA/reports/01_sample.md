# SEMMA Phase 1: Sample

## Problem Statement
Goal: Predict which students are "at risk" of poor final performance so that schools can intervene early.

We define "at risk" as a student whose final grade (`G3`) is below 10 out of 20.

## Data Source
We used the Student Performance dataset (UCI / Kaggle). It includes demographics, study time, absences, past grades, and final grades.

**Dataset size:** [REPLACE WITH df.shape] rows  
**Columns used for modeling:**
- age
- sex
- studytime
- absences
- failures (if available)
- G1 (first period grade)
- G2 (second period grade)

**Target variable (`at_risk`):**
- 1 = final grade G3 < 10
- 0 = final grade G3 ≥ 10

## Sampling and Partitioning
We created a modeling subset (`df_model`) using only the most relevant features for prediction and interpretability.

We then split into:
- Training set: 80%
- Test set: 20%
- `stratify=y` ensures the at-risk percentage is preserved in each split.

**Class balance in training set:**
- At risk: ~[y_train.mean()*100 rounded]% of students
- Not at risk: ~[100 - that number]%

## Why This Matters
This step ensures:
- We clearly know what we're predicting.
- We control for data imbalance early.
- We have a clean train/test setup for honest evaluation later.

## Risks / Assumptions
- G1/G2 are assumed to be known before the final exam (realistic in a school setting).
- Self-reported fields (like studytime) may be biased.
- The dataset might not generalize to all schools or districts.
