# Banking Customer Churn Analysis

Churn analysis of **10,000 retail-bank customers** with a **20.4% churn rate**: exploratory analysis of who leaves, then three classification models compared on their ability to catch churners before they go.

## Data

Customer-level banking dataset with demographics, credit score, geography, balance, product usage, activity status and salary. Target variable: `Exited` (1 = churned, 0 = stayed).

Features: `CreditScore`, `Geography`, `Gender`, `Age`, `Tenure`, `Balance`, `NumOfProducts`, `HasCrCard`, `IsActiveMember`, `EstimatedSalary`.

2,037 of 10,000 customers churned. Roughly one in five.

![Customer Churn Distribution](images/churn_distribution.png)

## Analysis

Cleaning dropped three identifier columns (`RowNumber`, `CustomerId`, `Surname`); the data had no missing values to impute. EDA compared churn rates across geography, gender, card ownership and activity status, then compared the numeric features between churners and stayers. Simple segments (age band, balance band, activity) translate the patterns into groups a retention team can act on.

![Churn Rate by Geography](images/churn_by_geography.png)

Correlation analysis ranked the drivers:

- **Age** has the strongest positive relationship with churn. Older customers leave more.
- **Balance** also relates positively to churn: high-balance customers are not safe customers.
- **Estimated salary** shows almost no relationship with churn.
- Credit score, tenure and number of products show weak negative relationships.

## Models

Logistic Regression, Random Forest and Gradient Boosting, trained to predict `Exited`:

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.81 | 0.59 | 0.19 | 0.28 |
| Random Forest | 0.86 | 0.76 | 0.45 | 0.57 |
| Gradient Boosting | 0.87 | 0.80 | 0.50 | 0.61 |

![Model Performance Comparison](images/model_comparison.png)

Gradient Boosting wins on every metric, and it still misses half of the customers who churn (recall 0.50). That gap matters more than the 0.87 accuracy: in retention, a missed churner is a lost customer, while a false positive costs one unnecessary retention offer. Any production use starts with raising recall, not accuracy.

## Recommendations for a retention team

1. **Watch older customers.** Age is the strongest churn signal in the data, so retention campaigns should weight age bands accordingly.
2. **Treat high balances as at-risk, not as loyal.** Balance correlates with churn, and these are the most expensive customers to lose.
3. **Re-engage inactive members.** Inactivity precedes churn; digital-banking nudges and personalized offers are the cheap first move.
4. **Target by predicted risk, not by blanket campaigns.** Even at recall 0.50, scoring customers with the Gradient Boosting model focuses the retention budget on the right half of future churners.

## Next steps

Threshold tuning for recall, hyperparameter optimization, feature engineering, and (the real unlock) transaction-level behavior data, which this dataset lacks.

## Repository structure

```text
banking-customer-churn-analysis/
├── README.md
├── requirements.txt
├── data/
│   └── churn.csv
├── images/
└── notebooks/
    └── banking_churn_analysis.ipynb
```

Tools: Python (pandas, NumPy, matplotlib, scikit-learn), Jupyter Notebook.

---

**Author:** Mukhammed Yesmukhanbet — MSc Management, Finance and Data Analytics (LUMSA, Rome)
[LinkedIn](https://www.linkedin.com/in/myesmukhanbet) · [GitHub](https://github.com/m-yesmukhanbet)
