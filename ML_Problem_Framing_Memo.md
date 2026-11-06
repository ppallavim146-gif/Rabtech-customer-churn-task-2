# ML Problem-Framing Memo — Customer Churn

## 1. Decision
The system is intended to support a customer-retention decision: identify customers who may be at higher risk of churn so a human/business team can decide whether follow-up is appropriate.

The model should support prioritization only. It must not automatically cancel, penalize, deny service, or make other high-impact decisions about a customer.

## 2. Prediction target
The target is `churned`.

- `1` = customer churned
- `0` = customer did not churn

## 3. Unit of observation
One row represents one customer.

The supplied starter dataset contains 12 customer records.

## 4. Action window
The intended action window is before a customer is expected to leave, using information that would have been available at prediction time.

The starter dataset does not contain a prediction timestamp, so the exact operational timing cannot be verified from the data alone.

## 5. Non-ML baseline
The non-ML baseline is a majority-class classifier.

In this dataset:
- 7 of 12 customers are labeled `0` (did not churn).
- 5 of 12 customers are labeled `1` (churned).
- Therefore, always predicting `0` gives a baseline accuracy of 7/12 = 58.3%.

This baseline is intentionally simple and provides a reference point for judging whether an ML model adds value.

## 6. Proposed ML approach
Use a simple, interpretable Logistic Regression model with:
- numerical features: `tenure_months`, `support_tickets`, `monthly_spend_inr`, `last_login_days`
- categorical feature: `plan_type`

`customer_id` is excluded because it is an identifier, not a useful behavioral feature.

## 7. Business and model metrics
Because the dataset is extremely small, accuracy alone is not sufficient.

The notebook reports:
- accuracy
- precision
- recall
- F1-score
- confusion matrix

For churn prediction, a false negative means a customer who churns is missed. A false positive means the business spends retention effort on a customer who would not have churned.

The relative business cost of these errors is not provided by the starter materials, so no unsupported monetary cost is assumed.

## 8. Abstention and human review
The model should not be treated as certain for every customer.

A proposed operational safeguard is:
- high-confidence prediction → candidate for normal retention workflow
- low-confidence prediction → human review
- any model/data quality failure → do not use the prediction; fall back to the approved non-ML process

The exact probability threshold should be validated with real operational data before deployment.

## 9. Monitoring and rollback
Before any real use, monitor:
- missing values and data schema changes
- class balance
- model performance over time
- false positives and false negatives
- calibration/confidence
- performance across relevant groups if such attributes become available and are appropriate to assess

Rollback condition:
If the model receives unexpected input, required features are missing, performance falls below an agreed threshold, or data quality checks fail, stop automated use and revert to the non-ML baseline/human process.

## 10. Important limitation
The supplied dataset has only 12 rows. It is suitable for a small responsible-baseline exercise, but it is not large enough to support a reliable production churn model or strong generalization claims.
