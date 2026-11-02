# credit-card-customer-spend-analytics
End-to-end credit card customer spending and financial behaviour analytics project using Python, Pandas, NumPy, exploratory data analysis, feature engineering, RFM customer segmentation, and Power BI interactive dashboards.

# Credit Card Customer Spend & Financial Behaviour Analytics

An end-to-end data analytics project using **Python and Power BI** to analyse credit card customer spending patterns, financial behaviour, customer segmentation, transaction frequency, income groups, geographic distribution, and credit score profiles.

## Project Overview

The objective of this project is to understand customer spending behaviour and identify meaningful business insights from transaction and customer-level data.

I developed this project from scratch, starting with data exploration and preparation in Python, followed by customer-level feature engineering, RFM-based customer segmentation, and interactive dashboard development in Power BI.

The project demonstrates how raw transaction data can be transformed into meaningful business insights that could support customer engagement, retention strategies, and financial analysis.

**Dataset Disclaimer:** This project uses a synthetic dataset sourced from Kaggle for educational and analytical purposes. It does not represent actual customers, transactions, or financial performance of any bank. No secondary dataset was used.

---

## Project Objectives

- Analyse customer credit card spending patterns.
- Understand transaction behaviour across different customer groups.
- Identify high-value and low-engagement customer segments.
- Perform customer segmentation using RFM analysis.
- Analyse spending patterns across income and age groups.
- Understand geographic spending distribution.
- Explore the relationship between credit scores and customer spending.
- Build interactive Power BI dashboards.
- Convert analytical findings into actionable business recommendations.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Data exploration, cleaning, transformation and feature engineering |
| Pandas | Data manipulation and aggregation |
| NumPy | Numerical operations and calculations |
| Jupyter Notebook | Python-based analysis and documentation |
| Power BI Desktop | Interactive dashboard development |
| Power Query | Data loading and transformation |
| DAX | Measures and business calculations |
| Git & GitHub | Version control and project documentation |

## Dataset Information

The project uses a synthetic credit card customer and transaction dataset obtained from Kaggle.

### Dataset size

| Description | Records |
|---|---:|
| Raw transaction records | 20,000 |
| Unique customers | 4,941 |
| Transaction date range | 01-Jan-2023 to 31-Oct-2025 |

### Transaction-level columns

The transaction dataset contains information such as:

- `id`
- `transaction_id`
- `date`
- `client_id`
- `card_id`
- `amount`
- `use_chip`
- `merchant_id`
- `merchant_city`
- `merchant_state`
- `zip`

### Customer-level attributes

The customer information includes:

- `client_id`
- `current_age`
- `birth_year`
- `birth_month`
- `gender`
- `address`
- `per_capita_income`
- `yearly_income`
- `total_debt`
- `credit_score`
- `num_credit_cards`

---

# Project Workflow

## Phase 1: Data Exploration Using Python

I started the project by loading the dataset into Python using Pandas.

The initial exploration included:

1. Understanding the dataset structure.
2. Checking the number of rows and columns.
3. Identifying column names and data types.
4. Reviewing statistical summaries.
5. Checking missing values.
6. Examining unique values in categorical columns.
7. Analysing numerical distributions.
8. Checking transaction date ranges.
9. Investigating repeated transaction IDs.
10. Examining customer and transaction distributions.

### Python libraries

```python
import pandas as pd
import numpy as np
```

### Initial dataset inspection

```python
df.head()
df.shape
df.info()
df.describe()
df.isnull().sum()
df.nunique()
```

### Duplicate analysis

I examined duplicate records and repeated transaction IDs separately.

```python
df.duplicated().sum()
df["transaction_id"].duplicated().sum()
```

A repeated transaction ID does not automatically mean that the entire row is duplicated. Therefore, I treated these as separate data-quality checks.

## Phase 2: Data Cleaning and Preparation

The next step was to prepare the dataset for analysis.

The data preparation process included:

- Reviewing missing values.
- Checking data types.
- Inspecting duplicate records.
- Validating customer identifiers.
- Reviewing categorical values.
- Converting date columns into appropriate date formats.
- Checking numerical columns for unusual values.
- Ensuring that customer-level and transaction-level data were suitable for analysis.

The objective was to improve data consistency and prepare reliable inputs for further analysis.

## Phase 3: Exploratory Data Analysis (EDA)

I performed exploratory analysis to understand customer characteristics and transaction behaviour.

### Customer demographic analysis

- Gender distribution.
- Age distribution.
- Age-group distribution.
- Yearly income distribution.
- Income-group distribution.
- Credit score distribution.

### Transaction analysis

- Transaction amount distribution.
- Transaction frequency.
- Spending by merchant state.
- Spending by merchant city.
- Transaction trends over time.
- Chip and non-chip transaction distribution.

### Statistical analysis

I used descriptive statistics such as:

- Mean
- Median
- Standard deviation
- Minimum and maximum
- Quartiles
- Skewness
- Correlation

I also explored the relationships between income, age, credit score, number of credit cards, total debt, and customer spending.

## Phase 4: Customer-Level Aggregation

The original transaction dataset contains multiple transactions for the same customer.

To understand customer behaviour, I created a customer-level summary by grouping transactions using `client_id`.

The resulting customer summary contained **4,941 customers and 15 columns**.

### Customer-level features

| Feature | Description |
|---|---|
| `client_id` | Unique customer identifier |
| `total_spend` | Total recorded spending per customer |
| `transaction_count` | Number of recorded transactions |
| `average_transaction_value` | Average spending per transaction |
| `first_transaction_date` | First recorded transaction date |
| `last_transaction_date` | Last recorded transaction date |
| `yearly_income` | Annual customer income |
| `per_capita_income` | Per-capita income attribute |
| `total_debt` | Customer debt attribute |
| `credit_score` | Customer credit score |
| `num_credit_cards` | Number of credit cards |
| `gender` | Customer gender |
| `current_age` | Customer age |
| `birth_year` | Customer birth year |
| `birth_month` | Customer birth month |

This aggregation allowed me to perform customer-level analysis rather than relying only on individual transactions.

## Phase 5: Feature Engineering

I created additional analytical features to make the dataset more useful for business analysis.

### 1. Transaction Frequency

Customers were grouped based on their recorded transaction counts.

| Category | Transaction count |
|---|---|
| Low | 1–2 |
| Moderate | 3–5 |
| High | 6–10 |
| Very High | More than 10 |

These are project-defined categories, not official banking standards.

### 2. Income Groups

I grouped customers according to their yearly income.

| Income group | Range |
|---|---|
| 0–3L | Up to ₹3 lakh |
| 3–6L | ₹3 lakh–₹6 lakh |
| 6–10L | ₹6 lakh–₹10 lakh |
| 10–15L | ₹10 lakh–₹15 lakh |
| 15–20L | ₹15 lakh–₹20 lakh |
| 20L+ | Above ₹20 lakh |

### 3. Age Groups

Customers were categorised into the following age ranges:

- 19–25
- 26–35
- 36–45
- 46–55
- 56–65
- 66–70

### 4. Recency Calculation

I calculated how many days had passed since each customer's last recorded transaction.

The analysis used 31 October 2025 as the reference date.

The recency groups were:

- 0–90 days
- 91–180 days
- 181–365 days
- 366–730 days
- 731+ days

These categories represent recorded transaction activity, not confirmed card inactivity or account closure.

## Phase 6: RFM Customer Segmentation

I applied RFM analysis to understand customer spending behaviour.

RFM stands for:

**Recency:** How recently a customer made a transaction.

**Frequency:** How many transactions a customer made.

**Monetary:** How much a customer spent in total.

I used these three dimensions to develop rule-based customer segments.

### Customer segments

- High-Value
- Active & Valuable
- Regular
- Low-Engagement

### Customer segment distribution

| Segment | Customers | Percentage |
|---|---:|---:|
| High-Value | 1,081 | 21.88% |
| Active & Valuable | 1,188 | 24.04% |
| Regular | 1,206 | 24.41% |
| Low-Engagement | 1,466 | 29.67% |
| **Total** | **4,941** | **100%** |

RFM was implemented as a rule-based segmentation approach, not a machine-learning model.

---

# Power BI Dashboard Development

After completing the Python analysis and feature engineering, I used Power BI Desktop to develop an interactive dashboard.

## Data Model

I used two analytical tables:

1. `transaction_data` – transaction-level information.
2. `customer_data_final` – customer-level summary information.

The tables were connected using the common `client_id` field.

The intended model is a one-to-many relationship:

- Customer table: One side.
- Transaction table: Many side.

This model helps separate customer-level attributes from transaction-level records.

## Dashboard Page 1: Customer Spending Overview

### Objective

To understand overall spending patterns and identify customer groups contributing significantly to recorded spending.

### KPI Cards

- Total Spend
- Total Transactions
- Total Customers
- Average Transaction Value

### Visualisations

1. Total spending by customer segment.
2. Customer count by customer segment.
3. Average spending by income group.
4. Average spending by age group.
5. Yearly income versus total spending scatter plot.

### Slicers

- Year
- Gender
- Income Group
- Age Group

### Business questions answered

- Which customer segment contributes the highest spending?
- Which income group has the highest average spending?
- Which age group has the highest average spending?
- How does customer income relate to recorded spending?
- How is spending distributed across customer segments?

## Dashboard Page 2: RFM Customer Segmentation Analysis

### Objective

To understand customer engagement, transaction frequency, recency, and monetary behaviour.

### KPI Cards

Customer count and customer segment indicators.

### Visualisations

1. Customer distribution by RFM segment.
2. Customer distribution by transaction frequency.
3. Customer distribution by recency groups.
4. RFM score distribution.
5. Transaction frequency versus total spending scatter plot.
6. Customer segment performance table.

### Slicers

- Gender
- Age Group
- Income Group
- Customer Segment

### Business questions answered

- Which customer segment contains the most customers?
- How many customers have low transaction frequency?
- Which customers have not made a recent recorded transaction?
- How does transaction frequency relate to spending?
- Which customer groups could be investigated for retention opportunities?

## Dashboard Page 3: Geographic & Credit Profile Analysis

### Objective

To analyse geographic spending patterns and understand customer distribution across credit score groups.

### KPI Cards

- Total Customers
- Total Spend
- Average Credit Score
- Average Spend per Customer

### Visualisations

1. Total spending by merchant city.
2. Geographic map showing spending by merchant state.
3. Customer distribution by credit score group.
4. Average spending by credit score group.
5. Credit score versus total spending scatter plot.

### Slicers

- Customer Segment
- Gender
- Age Group
- Income Group

### Business questions answered

- Which states and cities contribute the highest recorded spending?
- How are customers distributed across credit score groups?
- What is the average spending across credit score categories?
- Is there a relationship between credit score and spending?
- How does geographic spending vary across customer groups?

---

# Key Business Insights

## Insight 1: High-Value Customer Contribution

The High-Value segment represents approximately 21.88% of customers but contributes around 47.7% of total recorded spending.

**Business Recommendation:**

Banks could investigate personalised engagement, suitable rewards, and loyalty programmes for valuable customers. However, repayment behaviour, profitability, and risk should also be considered.

## Insight 2: Income Group and Spending Behaviour

The ₹6–10 lakh annual-income group contributes the highest total spending, while the ₹15–20 lakh income group has the highest average spending per customer.

**Business Recommendation:**

Financial institutions could explore different customer engagement strategies for different income groups. Larger customer groups may offer opportunities for broader engagement, while higher-average-spending groups may warrant more personalised offers.

## Additional Findings

- Total recorded spending is approximately ₹6.16 crore.
- Total transaction records: 20,000.
- Total unique customers: 4,941.
- Average transaction value: approximately ₹3,082.
- The correlation between credit score and total spending is approximately 0.017, indicating almost no linear relationship.
- The correlation between yearly income and total spending is approximately 0.285, indicating a weak positive relationship.
- The correlation between number of credit cards and total spending is approximately 0.537, indicating a moderately positive relationship in this dataset.

Correlation does not establish causation.

---

# Business Recommendations

Based on the analysis, the following opportunities could be investigated by a financial institution:

1. **Customer Retention:** Investigate the High-Value customer segment and explore appropriate retention strategies.
2. **Customer Engagement:** Examine customers with low recorded transaction frequency and understand possible reasons for reduced activity.
3. **Income-Based Strategies:** Explore different engagement strategies based on income-group spending patterns.
4. **Geographic Analysis:** Investigate geographic differences in spending to understand regional customer behaviour.
5. **Credit Profile Analysis:** Study the relationship between credit scores and spending alongside repayment and risk information.
6. **Further Financial Analysis:** Incorporate credit limits, outstanding balances, repayment history, and cost information for deeper financial analysis.

These are proposed business opportunities, not proven outcomes from campaign testing.

---

# Limitations of the Project

This project is based on a synthetic dataset and has several limitations.

- The dataset does not represent actual bank customers.
- No repayment-history information is available.
- Credit-limit information is not available.
- Fraud and default labels are not available.
- Merchant category information is not available.
- Actual bank revenue, expenses, and profit data are not available.
- Campaign response and conversion information is not available.

Therefore, this project does not perform credit-default prediction, fraud detection, bank profitability measurement, or future-spending prediction.

The findings should be treated as illustrative analytical results.

---

# Future Scope

The project could be extended by incorporating suitable additional data:

- Credit utilisation analysis.
- Repayment behaviour analysis.
- Customer delinquency analysis.
- Fraud detection using labelled transaction data.
- Customer churn modelling.
- Spending prediction.
- Campaign effectiveness analysis.
- Customer lifetime value analysis.
- Bank revenue and profitability analysis.

Predictive modelling would require appropriate historical data, target variables, and model evaluation.

---

# Project Structure

A suggested repository structure is:

```text
credit-card-customer-spend-analytics/
│
├── README.md
│
├── data/
│   ├── README.md
│   └── synthetic_dataset_source.txt
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   ├── 04_customer_aggregation.ipynb
│   ├── 05_feature_engineering.ipynb
│   └── 06_rfm_customer_segmentation.ipynb
│
├── powerbi/
│   └── Credit_Card_Customer_Analytics.pbix
│
├── dashboard_screenshots/
│   ├── customer_spending_overview.png
│   ├── rfm_customer_segmentation.png
│   └── geographic_credit_profile.png
│
└── requirements.txt
```

The filenames above are a suggested organisation. Update them to match the actual files you upload.

## Skills Demonstrated

- Python
- Pandas
- NumPy
- Data Cleaning
- Exploratory Data Analysis
- Descriptive Statistics
- Feature Engineering
- Customer Aggregation
- RFM Analysis
- Customer Segmentation
- Correlation Analysis
- Power BI
- Power Query
- DAX
- Data Modelling
- Data Visualisation
- Business Analysis
- Business Recommendations

## Acknowledgements

I would like to express my sincere gratitude to **Shivang Sir** for his valuable guidance, feedback, and support throughout this capstone project.

I am also thankful to **Imarticus Learning** for providing the learning environment and opportunity to apply my analytical skills through a practical project.

## Author

**Data Analytics | Python | Power BI | Business Intelligence**

This project represents my learning journey in transforming raw data into meaningful business insights.

---

**Disclaimer:** This project is intended solely for educational and portfolio purposes. The dataset is synthetic and sourced from Kaggle. The results do not represent actual bank customers, financial institutions, or real-world banking performance.
