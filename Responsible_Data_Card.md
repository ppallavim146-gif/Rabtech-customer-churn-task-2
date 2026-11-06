# Responsible Data Card

## Dataset purpose
This starter dataset may support a small educational experiment for predicting customer churn and prioritizing possible retention follow-up.

It must not be used as evidence for production deployment, automatic customer penalties, denial of service, account cancellation, or other high-impact decisions. The dataset is too small for such use.

## Provenance and permission
The file was supplied by RabTech Academy as the Customer Churn training dataset for this task.

The supplied materials do not document the original source system, collection process, individual consent status, licensing terms, or retention policy. These items should therefore be treated as unknown rather than assumed.

## Population and representation
The dataset contains 12 customer records.

Observed plan categories are:
- Basic
- Standard
- Pro

Churn labels:
- 7 customers: `churned = 0`
- 5 customers: `churned = 1`

The dataset is very small and may not represent the wider customer population. No information is supplied about geography, age, gender, income, accessibility, or other demographic groups. Therefore, representation and subgroup fairness cannot be established from this dataset.

## Features and target
| Feature | Meaning used in this exercise | Role / risk |
|---|---|---|
| `customer_id` | Customer identifier | Excluded from modeling; identifiers can create memorization/leakage risk |
| `tenure_months` | Customer tenure in months | Input feature |
| `support_tickets` | Number of support tickets | Input feature; timing/collection process is not documented |
| `monthly_spend_inr` | Monthly customer spend in INR | Input feature |
| `last_login_days` | Days since last login | Input feature; should only be used if available before the prediction decision |
| `plan_type` | Customer plan category | Input categorical feature; not identified as a sensitive attribute in the supplied materials |
| `churned` | Churn outcome | Target label; must not be used as an input feature |

Potential leakage:
- `customer_id` is excluded because it is an identifier.
- `churned` is the target and is excluded from input features.
- The dataset has no timestamps, so it is not possible to fully verify whether every feature would always be available before the prediction point. This is an important limitation.

## Quality checks
The supplied CSV contains:
- 12 rows
- 7 columns
- 0 missing values
- 0 duplicate rows
- 2 target classes
- 7 non-churned records and 5 churned records

The notebook performs these checks programmatically.

Outlier interpretation is limited because the dataset is extremely small. Numeric ranges should be reviewed rather than assuming that every unusual value is an error.

Train/test separation must be performed before evaluating the model. The notebook uses cross-validation for the ML baseline because the dataset is too small for a reliable single holdout estimate.

## Risks and safeguards

### Bias / representation risk
The dataset is too small and lacks demographic/context information, so fairness across real-world groups cannot be established.

**Safeguard:** Do not make subgroup fairness claims from this dataset. Reassess with representative production data before deployment.

### Privacy risk
The dataset contains a customer identifier.

**Safeguard:** Exclude `customer_id` from model training and avoid unnecessary exposure of customer-level information.

### Misuse risk
A churn score could be treated as a fact about a customer.

**Safeguard:** Use predictions only as decision support and keep a human in the loop.

### False-positive risk
A customer may be incorrectly flagged as likely to churn.

**Safeguard:** Avoid automatic expensive or punitive actions. Use human review and measure precision.

### False-negative risk
A customer who will churn may not be flagged.

**Safeguard:** Measure recall and monitor missed churn cases.

### Data-quality risk
Future data may contain missing fields, unexpected categories, or changed schemas.

**Safeguard:** Run input validation and stop model use when required checks fail.

### Data leakage risk
Information from after the prediction point could make the model look better than it really is.

**Safeguard:** Verify feature availability and timestamps before any real deployment.

## Intended evaluation
### Baseline
Majority-class baseline: always predict the most common class (`0` in this dataset).

### Model metrics
The notebook reports:
- accuracy
- precision
- recall
- F1-score
- confusion matrix

### Calibration
The model produces probabilities. Probability calibration should be evaluated on a larger, time-separated validation dataset before production use.

### Fairness
No sensitive attributes are supplied, so a meaningful subgroup fairness analysis cannot be completed for this starter dataset.

### Error analysis
Review false positives and false negatives and examine which input patterns are associated with each error.

## Intended use statement
This data card documents an educational baseline exercise. The dataset and model should not be interpreted as a production-ready churn system.
