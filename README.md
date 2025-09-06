

# FinTech Dataset Project – Milestone Report

## Introduction

The goal of this milestone is to load the provided CSV files, perform **Exploratory Data Analysis (EDA)** with visualization, extract additional data, perform **feature engineering**, and pre-process the dataset for downstream use cases such as **Machine Learning** and data analysis.

We are working with a **FinTech dataset**. It contains records about **customers, loans, and their corresponding loans**.

---

## 1. Exploratory Data Analysis (EDA)

### 1.1 Questions to Explore

1. What is the distribution of loan amounts among customers?
2. How many customers have defaulted on their loans?
3. How does annual income relate to loan amount?
4. What is the distribution of interest rates across different loan grades?
5. Are there specific months where more loans are issued?

### 1.2 Visualizations & Observations

*(Include plots here – histogram, boxplot, scatterplot, bar chart, etc.)*

* **Observation 1:** The majority of loans are concentrated in the lower range (X-Y).
* **Observation 2:** Default rate is higher in lower-income groups.
* **Observation 3:** Annual income tends to increase with higher loan amounts but outliers exist.
* **Observation 4:** Loan grade A has the lowest interest rate, while grade G has the highest.
* **Observation 5:** Most loans are issued in March and September, indicating possible seasonal patterns.

---

## 2. Data Cleaning

### 2.1 Column Names

* Tidied all column names (removed spaces, special characters).
* Example: `Loan Amount` → `loan_amount`.

### 2.2 Index Selection

* Selected **Customer ID** as the index for unique identification.

### 2.3 Handling Inconsistent Data

* Standardized text values (e.g., `INDIVIDUAL` → `Individual`).
* Removed duplicates and irrelevant columns.

### 2.4 Handling Missing Data

* **Observation:** Missing data patterns suggest MCAR and MAR types.
* **Action:** Imputed missing `age` values based on loan grade averages; missing categorical values filled with mode.
* **Comment:** Imputation reduces bias while preserving data distribution.

### 2.5 Outliers

* Observed outliers in `loan_amount` and `annual_income` using boxplots.
* Handled by **capping at 1st and 99th percentiles** to avoid distortion in ML models.

---

## 3. Data Transformation and Feature Engineering

### 3.1 Added Columns

1. **Month Number:**

   * Extracted month from `issue_date`.
   * Datatype converted to `datetime`.

2. **Salary Can Cover:**

   * Boolean column indicating if annual income covers loan amount (`True`=1, `False`=0).

3. **Letter Grade:**

   * Encoded grades A–G as categorical variables.

4. **Installment per Month (M):**

   $$
   M = P \times \frac{r(1 + r)^n}{(1 + r)^n - 1}
   $$

   * `P` = loan principal, `r` = monthly interest rate, `n` = number of payments.

### 3.2 Categorical Encoding

* Used **one-hot encoding** for categorical features.
* Comment: This prevents the model from assuming ordinal relationships where none exist.

### 3.3 Normalization

* `loan_amount` and `annual_income` normalized using **Min-Max scaling** to bring all features into the 0–1 range.


## 4. Lookup Table(s)

* Created programmatic **CSV lookup table** for all encoded and imputed values.
* Examples:

| Original Value | Encoded Value | Description                                    |
| -------------- | ------------- | ---------------------------------------------- |
| Individual     | 1             | Customer type                                  |
| -1             | -1            | Missing annual income imputed by grade average |

* Purpose: To reverse encoded or imputed values if needed.


## 5. Summary

* Completed **EDA** and answered 5 key questions.
* Cleaned the dataset: removed inconsistencies, handled missing values, and capped outliers.
* Engineered new features to enhance predictive power.
* Encoded categorical features and normalized numerical features.
* Created **lookup tables** for transparency and reproducibility.

This dataset is now ready for **Machine Learning models** or further **data analysis**.

