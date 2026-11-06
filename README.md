# RabTech Academy — Task 2: ML Problem Framing & Responsible Data Card

## Files
- `customer-churn-training.csv` — RabTech starter dataset
- `ML_Problem_Framing_Memo.md` — problem framing
- `Responsible_Data_Card.md` — completed data card
- `Risk_Register.md` — risk register
- `customer_churn_baseline.ipynb` — baseline analysis and ML notebook

## Run the notebook in VS Code

1. Open this folder in VS Code.
2. Make sure Python 3.10+ is installed.
3. Install the required packages in the VS Code terminal:

```bash
python -m pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

4. Open `customer_churn_baseline.ipynb`.
5. Select a Python kernel/interpreter.
6. Run the cells from top to bottom.
7. Do not change the CSV filename unless you move/rename the dataset.
8. Review the printed checks and metrics before submitting.

## Important interpretation
The dataset contains only 12 rows. The notebook is intentionally a small responsible-baseline exercise, not a production model.

The notebook compares:
1. A majority-class non-ML baseline.
2. A simple Logistic Regression model.

Because the dataset is very small, model metrics can be unstable. Do not claim that the model is production-ready.
