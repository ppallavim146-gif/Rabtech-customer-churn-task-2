# Risk Register — Customer Churn ML Baseline

| ID | Risk | Impact | Mitigation / safeguard | Status |
|---|---|---|---|---|
| R1 | Dataset is extremely small (12 rows) | Model performance may be unstable and may not generalize | Treat results as educational only; validate on a much larger representative dataset before deployment | Open |
| R2 | Unknown original provenance/consent | Data-use and privacy requirements cannot be fully verified | Record provenance as unknown where not documented; verify source, permission and licensing before real use | Open |
| R3 | Customer identifier used as a feature | Memorization or leakage risk | Exclude `customer_id` from modeling | Mitigated |
| R4 | False positive | Retention effort may be spent on a customer who would not churn | Monitor precision; require human review; avoid automatic high-cost actions | Open |
| R5 | False negative | A customer likely to churn may be missed | Monitor recall and missed-churn cases | Open |
| R6 | Temporal leakage | Model could use information that was only known after the prediction point | Verify feature availability and timestamps before deployment | Open |
| R7 | Missing/invalid future inputs | Predictions may become unreliable | Validate schema, required fields and categories before prediction | Open |
| R8 | Class distribution changes | Model performance may degrade over time | Monitor target distribution and retrain/revalidate when appropriate | Open |
| R9 | Unsupported fairness claims | Model may work differently for groups not represented in the dataset | Do not claim fairness from this dataset; perform subgroup evaluation with appropriate data before deployment | Open |
| R10 | Over-trusting model probability | Users may treat a prediction as certainty | Use confidence thresholds and human review; document uncertainty | Open |
| R11 | Model degradation | Model may become inaccurate after deployment | Monitor agreed performance metrics and define rollback thresholds | Open |
| R12 | Incorrect use of churn prediction | Prediction could be used for punitive or high-impact decisions | Restrict intended use to decision support and retention prioritization | Open |

## Abstention / human-review rule
If required input data is missing, unexpected categories are present, the model fails validation, or the prediction confidence is too low for an agreed operational threshold, the system should abstain and route the case to the existing human/non-ML process.

## Rollback rule
Stop model-assisted decisions and use the approved non-ML baseline if data validation fails or monitored performance falls below the pre-agreed operational threshold.
