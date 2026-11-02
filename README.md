# Smart Customer Churn & Retention Intelligence System

An end-to-end machine learning project that predicts which customers are likely to churn, ranks them by revenue at risk, and recommends a retention action for each one.

> **Data disclosure:** this project uses a **simulated** 12,000-customer telecom-style dataset, not real customer records. Churn outcomes are sampled from a probability model with built-in relationships. The scores below demonstrate the workflow and must **not** be read as performance on real customers.

## Why this project

Keeping a customer is usually cheaper than winning a new one, but a retention team has limited time. This project answers three questions:

1. **Who** is likely to leave?
2. **How much** revenue is at stake?
3. **What** should the team do for each customer?

## What it does

- Generates a reproducible 12,000-customer dataset (fixed random seed 42) with 11 input features.
- Runs data-quality checks and exploratory analysis.
- Splits the data 70 / 15 / 15 into train, validation and test sets, stratified by churn.
- Compares three models: Logistic Regression, Random Forest and CatBoost.
- Selects the model on validation PR-AUC and the decision threshold on validation data only.
- Evaluates once on an untouched test set.
- Scores every customer, assigns a risk band and a recommended action, and exports a CSV for Power BI.

## Results

**Model comparison (validation set)**

| Model | Accuracy (0.50) | ROC-AUC | PR-AUC |
|---|---|---|---|
| **CatBoost (selected)** | 0.8311 | 0.8685 | 0.6731 |
| Logistic Regression | 0.8311 | 0.8655 | 0.6679 |
| Random Forest | 0.8106 | 0.8545 | 0.6408 |

**Final test set (1,800 unseen customers, threshold 0.355)**

| Accuracy | Precision | Recall | F1 | ROC-AUC | PR-AUC |
|---|---|---|---|---|---|
| 81.22% | 59.46% | 62.56% | 60.97% | 0.8554 | 0.6838 |

Confusion matrix: 1,198 true negatives, 180 false positives, 158 false negatives, 264 true positives. The test churn rate is 23.44%, so the no-skill PR-AUC baseline is 0.234.

The threshold was set on validation data as the highest accuracy with at least 65% recall. Test recall landed slightly lower at 62.6%, which is reported as it came out.

**Top churn drivers (CatBoost feature importance)**

| Rank | Feature | Importance |
|---|---|---|
| 1 | Customer satisfaction | 24.7 |
| 2 | Support tickets | 14.9 |
| 3 | Contract type | 11.0 |
| 4 | Late payments | 9.8 |
| 5 | Tenure (months) | 8.9 |

Month-to-month customers churn at 28.7%, against 20.1% on one-year and 12.8% on two-year contracts.

**Risk bands and actions (all 12,000 customers)**

| Risk band | Customers | Share | Annual charge exposure |
|---|---|---|---|
| High (above 50%) | 1,879 | 15.7% | 1,224,028 |
| Medium (25% to 50%) | 2,175 | 18.1% | 725,702 |
| Low (below 25%) | 7,946 | 66.2% | 652,658 |

High-risk customers are 15.7% of the base but hold about 47% of the annual charge exposure.

| Recommended action | Customers |
|---|---|
| Priority service recovery call | 674 |
| Billing support and payment plan review | 404 |
| Personalised retention offer | 801 |
| Engagement and satisfaction check-in | 2,175 |
| Standard service; monitor | 7,946 |

## Repository contents

| File | Description |
|---|---|
| `Customer_Retention_Advanced.ipynb` | Full notebook: data, models, evaluation, scoring |
| `customer_retention_predictions.csv` | Customer-level output: probability, risk band, action, exposure (12,000 rows, 19 columns) |
| `Smart_Churn_Retention_Report.pdf` | 7-page project report |

## How to run

```bash
git clone https://github.com/kevinn7305/Smart-Customer-Churn-and-Retention-Intelligenece-System-using-Machine-Learning-.git
cd Smart-Customer-Churn-and-Retention-Intelligenece-System-using-Machine-Learning-
pip install numpy pandas matplotlib scikit-learn catboost jupyter
jupyter notebook Customer_Retention_Advanced.ipynb
```

Run all cells. The notebook regenerates the dataset, trains the models and writes `customer_retention_predictions.csv`. Results are reproducible because of the fixed seed.

## Output columns

`customer_id`, the 11 input features, `churn` (simulated outcome), `churn_probability`, `churn_probability_pct`, `risk_category`, `recommended_action`, `estimated_annual_charge_exposure`, `retention_priority_score`.

`estimated_annual_charge_exposure` is monthly charges × 12 × churn probability. It is a prioritisation proxy, not a forecast of recoverable revenue.

## Power BI

Load `customer_retention_predictions.csv` and build views on `risk_category`, `recommended_action` and `retention_priority_score` to give a retention team a ranked call list.

## Limitations

- **Simulated data.** Results apply only to this simulation, not to real customers.
- **Built-in signals.** The churn relationships were designed into the data, which makes the task easier than real data. The model recovering them is a workflow check, not a discovery.
- **Random split.** A real deployment needs time-based splits.
- **Importance is not causation.** Feature importance shows what the model uses, not what causes churn.
- **Threshold.** It was set on accuracy and recall. A real campaign should use cost against customer value.

## Next steps

- Repeat the experiment on a documented real dataset, such as IBM's public Telco Customer Churn sample.
- Add cost-sensitive thresholds, fairness checks and drift monitoring.
- Build and publish the Power BI dashboard.

## Tech stack

Python, pandas, NumPy, scikit-learn, CatBoost, matplotlib.

## Author

**Kevinn**, business analytics. Feedback and suggestions are welcome.
