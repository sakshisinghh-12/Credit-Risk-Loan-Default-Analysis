# Credit-Risk-Loan-Default-Analysis
Case Study using Python, MySQL,  Pandas, Seaborn

# Project Overview

This project analyzes a real-world credit risk dataset of ~150,000 borrowers to identify which financial characteristics are most strongly associated with loan default. Rather than building a machine learning model, the focus is on building an analytical narrative — the kind of quantified, segment-level insight that a credit analyst would present to a risk committee.

The dataset used is the "Give Me Some Credit" dataset from Kaggle, which contains borrower-level data including monthly income, credit utilization, debt ratio, age, number of late payments, and a binary default flag.

# Business Problem
Lenders lose money when borrowers default. Identifying who is likely to default — and why — before a loan goes bad is one of the most valuable problems in financial analytics. This project attempts to answer:

Which borrower segments carry the highest default risk, and what financial signals best predict it?

# Tools & Technologies
Python 3 : Core analysis language

Pandas : Data cleaning, aggregation, segmentation

Seaborn + Matplotlib : All visualizations

MySQL : Storing cleaned data, running SQL queries

SQLAlchemy : Python-to-MySQL connection

Jupyter Notebook : Analysis environment

# Methodology

#Step 1 — Data Cleaning

The raw dataset had several real-world issues that needed to be handled before any analysis:

29,731 missing income values (19.8%) → Filled with median income ($5,400)

3,924 missing dependent values → Filled with 0

DebtRatio outliers (max: 329,664 — impossible) → Capped at 10

RevolvingUtilization outliers (max: 50,708) → Capped at 1.0

Age = 0 rows → Removed entirely

MonthlyIncome extreme values → Capped at 99th percentile ($23,000)

Final dataset: 149,986 rows, 11 columns, zero missing values.

# Step 2 — Feature Engineering

Created four grouping columns to enable segment-level analysis:

AgeBand — 6 age groups (21-30, 31-40, 41-50, 51-60, 61-70, 71+)

IncomeBand — 4 income groups (<$3K, $3K-$6K, $6K-$10K, >$10K)

UtilizationGroup — 4 utilization groups (0-30%, 30-60%, 60-80%, 80-100%)

DebtRatioGroup — 4 debt ratio groups

RiskScore — A rule-based 0–5 score built from 5 risk flags

# Step 3 — Exploratory Analysis

Calculated default rates across all segments using Pandas groupby() aggregations. Combined segments (income × utilization) to identify the highest-risk borrower profiles.

#Step 4 — Visualizations

Bar charts for default rate by age, income, utilization, and risk score

Scatter plot of debt ratio vs monthly income colored by default status

Heatmap of default rate across income × utilization combinations

# Step 5 — SQL Analysis
Loaded the cleaned dataset into a local MySQL database and ran 5 queries:

Overall default rate

Default rate by age band (GROUP BY)

Top 20 highest-risk borrowers (ORDER BY RiskScore DESC)

Default rate by income + utilization segment (multi-column GROUP BY)

Default rate by risk score with RANK() window function


# Visualizations
Default Rate by Age Band:
Younger borrowers (21-30) default at nearly twice the rate of the overall portfolio.

Default Rate by Credit Utilization:
The strongest signal in the dataset. Borrowers above 80% utilization default at 21% — nearly 9.5x those with low utilization.

Income × Utilization Heatmap:
The combined effect: low income + very high utilization produces a 22.56% default rate, the worst segment in the dataset.

Risk Score Validation:
The custom 5-point risk score shows a near-perfect gradient from 1.74% (score 0) to 57.74% (score 5), confirming the chosen risk factors are genuinely predictive.
