
# Transaction Risk Scoring — Feature Engineering & Baseline Modeling

A machine learning project focused on identifying potentially fraudulent transactions through exploratory data analysis, SQL analysis, feature engineering, classification modeling, risk scoring, and model interpretability.

## Project Overview

This project develops a baseline transaction risk scoring workflow using Python, Pandas, Scikit-Learn, SQL, and SHAP.

The workflow covers:

* Transaction data cleaning and exploratory analysis
* Feature engineering
* SQL-based transaction analysis using SQLite
* Fraud classification
* Comparison of Logistic Regression, Random Forest, and Gradient Boosting
* Model evaluation using Precision, Recall, F1, ROC-AUC, and PR-AUC
* SHAP-based model interpretability
* Transaction-level fraud probability and risk scoring
* Risk categorization
* Classification threshold analysis
* Visualization of model and risk insights

## Tech Stack

* Python
* Pandas
* NumPy
* Scikit-Learn
* Matplotlib
* SHAP
* SQLite
* SQL
* Jupyter Notebook

## Project Workflow

### 1. Data Preparation

The dataset was cleaned by handling missing target values and filling missing numerical feature values using median imputation.

Additional features were created from transaction information, including:

* `log_amount`
* `time_hours`
* `time_hour`

The log transformation was applied to transaction amounts to reduce skewness.

### 2. Exploratory Data Analysis

The analysis examined:

* Fraud vs. legitimate transaction distribution
* Transaction amount distributions
* Fraud rates by transaction hour
* Fraud rates across transaction amount buckets
* Differences in transaction-level features between fraudulent and legitimate transactions

### 3. SQL Analysis

The transaction data was loaded into SQLite to perform analytical queries.

SQL analysis included:

* Total transaction counts
* Fraud and legitimate transaction counts
* Fraud rates by transaction amount bucket
* Fraud rates by transaction hour
* High-value transaction analysis
* Fraud transaction analysis
* Summary statistics for transaction amounts

### 4. Machine Learning

Three classification models were evaluated:

1. Logistic Regression
2. Random Forest
3. Gradient Boosting

The dataset was split into training and testing sets using stratified sampling to preserve the highly imbalanced fraud distribution.

### 5. Model Evaluation

The models were evaluated using metrics appropriate for fraud detection:

* Precision
* Recall
* F1 Score
* ROC-AUC
* PR-AUC
* Confusion Matrix

The recorded test-set results were:

| Model               | Precision | Recall |   F1 | ROC-AUC | PR-AUC |
| ------------------- | --------: | -----: | ---: | ------: | -----: |
| Logistic Regression |      0.11 |   0.90 | 0.20 |  0.9520 | 0.5309 |
| Random Forest       |      0.93 |   0.67 | 0.78 |  0.9997 | 0.9402 |
| Gradient Boosting   |      0.89 |   0.81 | 0.85 |  0.9897 | 0.7764 |

Because fraud detection involves substantial class imbalance, both ROC-AUC and PR-AUC were considered alongside precision, recall, and F1.

### 6. Model Interpretability

SHAP was used to investigate which features contributed most to the Random Forest predictions.

The notebook includes:

* SHAP summary plots
* Mean absolute SHAP feature importance
* Individual transaction explanations
* Top feature analysis

This provides additional interpretability beyond aggregate model performance metrics.

### 7. Risk Scoring

Random Forest fraud probabilities were converted into transaction-level risk scores:

```text
Risk Score = Fraud Probability × 100
```

Transactions were then categorized as:

| Risk Score | Category  |
| ---------: | --------- |
|       < 30 | Low       |
|   30–49.99 | Medium    |
|   50–79.99 | High      |
|       ≥ 80 | Very High |

The notebook also analyzes observed fraud rates and fraud capture rates across these categories.

### 8. Threshold Analysis

The project evaluates different classification thresholds to examine the trade-off between:

* Precision
* Recall
* F1 Score

A threshold of `0.30` was also evaluated as part of the threshold analysis.

## Key Visualizations

The project includes visualizations for:

* Fraud vs. legitimate transactions
* Transaction amount distributions
* Fraud rates by hour
* Fraud rates by transaction amount
* Model comparison
* SHAP feature importance
* Precision/Recall/F1 threshold analysis
* Risk category fraud rates
* Confusion matrix


## Disclaimer

This project is intended for educational and portfolio purposes. The model represents a baseline fraud-risk scoring workflow and should not be treated as a production fraud detection system without additional validation, monitoring, calibration, and domain-specific evaluation.
