# Smart Customer Churn & Retention Intelligence System

## Project Overview

Customer churn is a major challenge for subscription-based and service-oriented businesses. Losing existing customers can negatively affect revenue, profitability, and long-term customer relationships.

This project develops a **Machine Learning-based Customer Churn and Retention Intelligence System** that goes beyond traditional churn prediction.

Instead of only predicting whether a customer is likely to churn, the project also:

- Predicts customer churn probability
- Categorizes customers based on churn risk
- Identifies financially valuable customers at risk
- Creates a customer priority score
- Estimates customer value at risk
- Recommends targeted retention actions

The objective is to transform machine learning predictions into actionable business insights that can support customer retention decisions.

---

# Business Problem

Businesses often have limited resources for customer retention campaigns. Contacting every customer with the same retention strategy can be inefficient and expensive.

Therefore, the key business questions addressed in this project are:

1. Which customers are most likely to churn?
2. Which model performs better for predicting churn?
3. Which customers should be prioritized for retention?
4. Which financially valuable customers are at risk?
5. What retention action can be recommended?
6. How much customer value is potentially at risk?

---

# Project Objectives

The main objectives of this project are to:

- Develop machine learning models to predict customer churn
- Compare Logistic Regression and Random Forest models
- Evaluate models using multiple performance metrics
- Select the most suitable model based on ROC-AUC
- Generate churn probabilities for individual customers
- Segment customers into risk categories
- Develop a customer priority score
- Estimate potential customer value at risk
- Recommend business retention actions
- Prepare the final dataset for business intelligence and dashboard development

---

# Dataset

A synthetic customer dataset containing **1,000 customer records** was created for this project.

The dataset includes the following variables:

| Feature | Description |
|---|---|
| `customer_id` | Unique identifier for each customer |
| `tenure_months` | Number of months the customer has been associated with the company |
| `monthly_charges` | Monthly charges paid by the customer |
| `total_spend` | Total amount spent by the customer |
| `support_tickets` | Number of customer support tickets raised |
| `late_payments` | Number of late payments |
| `monthly_usage_hours` | Monthly service usage |
| `contract_type` | Customer contract type |
| `churn` | Target variable indicating customer churn |

## Target Variable

- `0` = Customer did not churn
- `1` = Customer churned

The synthetic churn variable was generated based on selected customer characteristics and risk factors.

---

# Project Workflow

```text
Customer Dataset
       ↓
Data Exploration
       ↓
Data Preprocessing
       ↓
Train-Test Split
       ↓
Logistic Regression
       ↓
Random Forest
       ↓
Model Comparison
       ↓
Best Model Selection
       ↓
Churn Probability Prediction
       ↓
Risk Categorization
       ↓
Retention Recommendations
       ↓
Customer Priority Score
       ↓
Estimated Value at Risk
       ↓
Business Intelligence Output
```

---

# Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- Machine Learning

---

# Machine Learning Models

## 1. Logistic Regression

Logistic Regression was used as the baseline model for the binary customer churn classification problem.

The model predicts whether a customer is likely to churn based on customer characteristics and behavior.

---

## 2. Random Forest Classifier

Random Forest was used to capture more complex and non-linear relationships between customer characteristics and churn behavior.

The model was configured using multiple decision trees and compared with Logistic Regression.

---

# Model Performance Results

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC Score

## Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.6850 | 0.5000 | 0.1905 | 0.2759 | **0.6201** |
| Random Forest | **0.6900** | **0.5172** | **0.2381** | **0.3261** | 0.5937 |

---

# Best Model Selection

Although Random Forest achieved slightly better results in Accuracy, Precision, Recall, and F1 Score, Logistic Regression achieved the higher ROC-AUC score.

## Selected Model

**Logistic Regression**

## ROC-AUC Score

**0.6201**

ROC-AUC was used as the primary model selection metric because this project focuses not only on classifying customers but also on generating churn probabilities for customer prioritization.

---

# Customer Risk Categorization

Customers were categorized based on their predicted churn probability.

| Risk Category | Churn Probability |
|---|---|
| High Risk | 75% and above |
| Medium Risk | 50% to 74.99% |
| Low Risk | Below 50% |

## Risk Category Results

| Risk Category | Number of Customers |
|---|---:|
| Low Risk | 884 |
| Medium Risk | 116 |
| High Risk | 0 |

The model classified the majority of customers as low risk, with 116 customers identified as medium risk.

No customers reached the current 75% threshold for the High Risk category.

---

# Overall Business Results

The final analysis produced the following results:

| Metric | Result |
|---|---:|
| Total Customers | 1,000 |
| High-Risk Customers | 0 |
| Medium-Risk Customers | 116 |
| Low-Risk Customers | 884 |
| Average Churn Probability | 31.24% |
| Estimated Total Value at Risk | 14,711,359.13 |

The results indicate that although no customers crossed the current high-risk threshold, a group of medium-risk customers should still be monitored and considered for proactive retention activities.

---

# Customer Priority Score

Not every customer with churn risk has the same financial importance.

A customer priority score was calculated using:

```text
Priority Score = Churn Probability × Total Customer Spend
```

Customers with higher priority scores have both:

- A higher probability of churn
- Greater financial value to the company

This helps businesses prioritize customers based on both risk and financial importance.

---

# Estimated Customer Value at Risk

The estimated value at risk was calculated using:

```text
Estimated Value at Risk = Total Customer Spend × Churn Probability
```

The total estimated customer value at risk across the dataset was:

**14,711,359.13**

This metric provides a business-oriented estimate of the potential customer value associated with predicted churn risk.

---

# Top Priority Customer Insight

The highest-priority customer was identified by combining churn probability with total customer spending.

### Customer Details

- **Customer ID:** 109
- **Churn Probability:** 56.73%
- **Total Spend:** 98,359
- **Priority Score:** 55,803.43
- **Risk Category:** Medium Risk
- **Recommended Action:** Discount or Engagement Campaign

This demonstrates why customer prioritization is important.

A customer does not necessarily need to be classified as High Risk to require business attention. A Medium-Risk customer with high financial value can still represent significant potential value at risk.

---

# Customer Retention Recommendations

The project includes a rule-based recommendation system that converts churn predictions into potential retention strategies.

Possible recommendations include:

- Priority Customer Support
- Flexible Payment Plan
- Personalized Retention Offer
- Discount or Engagement Campaign
- No Immediate Action

For the highest-priority customers identified in the analysis, the primary recommendation was:

**Discount or Engagement Campaign**

---

# Key Findings

The major findings from the project are:

- Logistic Regression achieved the highest ROC-AUC score of **0.6201** and was selected as the final model.
- Random Forest achieved slightly higher Accuracy, Precision, Recall, and F1 Score than Logistic Regression.
- The average predicted churn probability across customers was **31.24%**.
- **116 customers** were categorized as Medium Risk.
- **884 customers** were categorized as Low Risk.
- No customers crossed the current 75% threshold for High Risk.
- The estimated total customer value at risk was approximately **14.71 million**.
- Customer prioritization identified financially valuable Medium-Risk customers who may require proactive retention strategies.
- Combining churn probability with customer spending provides more useful business insights than churn classification alone.

---

# Business Value

This project demonstrates how machine learning can be integrated with business analytics.

Instead of stopping at customer churn prediction, the project converts predictions into actionable business intelligence.

The system helps businesses:

- Identify customers with elevated churn risk
- Prioritize financially valuable customers
- Estimate potential customer value at risk
- Recommend appropriate retention actions
- Support data-driven customer retention decisions

The project focuses on answering the following business question:

> **Which customers should the company prioritize, and what action should be considered to reduce potential customer churn?**

---

# Project Structure

```text
Smart-Customer-Churn-Retention-Intelligence/
│
├── Customer_Retention.ipynb
│
├── customer_churn_predictions.csv
│
└── README.md
```

---

# How to Run the Project

## 1. Clone the Repository

```bash
git clone <repository-url>
```

## 2. Navigate to the Project Directory

```bash
cd Smart-Customer-Churn-Retention-Intelligence
```

## 3. Install Required Libraries

```bash
pip install pandas numpy matplotlib scikit-learn
```

## 4. Open the Jupyter Notebook

Open:

```text
Customer_Retention.ipynb
```

Run all cells sequentially from top to bottom.

---

# Project Output

The final output dataset contains:

- Customer ID
- Customer characteristics
- Actual churn information
- Predicted churn probability
- Churn probability percentage
- Customer risk category
- Recommended retention action
- Customer priority score
- Estimated customer value at risk

The final dataset is exported as:

```text
customer_churn_predictions.csv
```

---

# Future Improvements

Potential future improvements include:

- Using a real-world customer churn dataset
- Hyperparameter tuning using GridSearchCV or RandomizedSearchCV
- Testing Gradient Boosting and XGBoost models
- Adjusting churn risk thresholds based on business requirements
- Handling potential class imbalance using SMOTE or other resampling techniques
- Explainable AI using SHAP
- Developing an interactive Power BI dashboard
- Deploying the model using Streamlit
- Creating an automated churn monitoring system

---

# Author

**Kevinn Infan Benedick B**

MSc Business Analytics  
Manipal School of Commerce and Economics

---

# Project Summary

This project demonstrates an end-to-end machine learning and business analytics workflow:

**Data Generation → Data Exploration → Data Preprocessing → Model Training → Model Evaluation → Churn Probability Prediction → Risk Segmentation → Customer Prioritization → Retention Recommendations → Business Insights**

The project demonstrates that customer churn analysis becomes more valuable when predictive modeling is combined with customer value and actionable business recommendations.
