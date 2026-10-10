   # Fraud Detection API

   Detects fraudulent credit card transactions in real time and serves predictions through a REST API.

   ## Problem
   Fraud is very rare (~0.17% of transactions), so accuracy is a misleading metric.

   ## Dataset
   Kaggle "Credit Card Fraud Detection" (ULB) - 284,807 transactions, 492 frauds.

   ## Approach
1. EDA: 284,807 transactions, 492 fraud (0.173%), no missing values.
2. Stratified 80/20 train-test split so both halves keep the fraud rate.
3. StandardScaler fitted on training data only (avoids data leakage).
4. Baseline: logistic regression with class_weight="balanced".
5. Next: XGBoost with scale_pos_weight, then threshold tuning, then a FastAPI service.

## Results
| Model | PR-AUC | Recall | Precision | Frauds caught | Accuracy |
|---|---|---|---|---|---|
| Always predict "not fraud" | 0.0017 | 0.000 | - | 0 / 98 | 99.83% |
| Logistic regression (baseline) | 0.719 | 0.918 | 0.061 | 90 / 98 | 97.55% |

The baseline has *lower accuracy* than doing nothing, and is far more useful.
It catches 90 of 98 frauds but raises 1,386 false alarms, so the next steps are
a stronger model and a cutoff chosen by cost rather than 0.5.

   ## How to run
   TBD