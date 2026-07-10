# A-B Test - Data Cleaning

**Cohort:** Cohort-2  
**Owner:** Bhawana

## Purpose
Load the raw dataset, handle missing values, fix data types, remove duplicates, and export a clean dataset the rest of the team can use.

# 📊 Data Cleaning – Stock Market Dataset

## Project Overview

This project focuses on cleaning and preparing a historical stock market dataset for further statistical analysis and exploratory data analysis (EDA). The dataset contains daily trading information for Apple (AAPL), Microsoft (MSFT), and SPY ETF.

The objective of the data cleaning process was to improve data quality, ensure consistency, and prepare the dataset for reliable statistical analysis and visualization.

---

# Dataset Information

The dataset contains the following features:

| Column | Description |
|--------|-------------|
| Date | Trading date |
| Open | Opening stock price |
| High | Highest stock price of the day |
| Low | Lowest stock price of the day |
| Close | Closing stock price |
| Adj Close | Adjusted closing price |
| Volume | Number of shares traded |
| Stock_Name | Name of the stock (AAPL, MSFT, SPY) |

---

# Data Cleaning Objectives

The primary objectives of the data cleaning process were:

- Improve data quality
- Handle missing values
- Remove duplicate records
- Ensure correct data types
- Standardize column names
- Prepare the dataset for statistical analysis and EDA

---

# Data Cleaning Steps Performed

## 1. Imported Required Libraries

The following Python libraries were used:

- Pandas
- NumPy

---

## 2. Loaded the Dataset

The raw dataset was imported into a Pandas DataFrame for preprocessing.

---

## 3. Dataset Inspection

Initial inspection was performed using:

- `head()`
- `tail()`
- `shape`
- `columns`
- `info()`

This helped understand the structure and contents of the dataset.

---

## 4. Missing Value Analysis

Missing values were identified using:

```python
df.isnull().sum()
```

Appropriate handling techniques were applied depending on the column type.

---

## 5. Duplicate Record Check

Duplicate rows were identified using:

```python
df.duplicated().sum()
```

Duplicate records were removed if present.

---

## 6. Data Type Validation

The data types of all columns were verified using:

```python
df.info()
```

The **Date** column was converted into datetime format for time-series analysis.

---

## 7. Column Name Standardization

Column names were checked and standardized to improve readability and maintain consistency.

---

## 8. Final Dataset Verification

The cleaned dataset was verified by checking:

- Missing values
- Duplicate records
- Data types
- Dataset dimensions

---

# Final Clean Dataset

The cleaned dataset contains:

- No duplicate records
- Proper data types
- Consistent formatting
- Clean column names
- Data ready for statistical analysis and visualization

---

# Tools Used

- Python
- Pandas
- NumPy
- Google Colab

---

# Outcome

The cleaned dataset serves as a reliable foundation for:

- Descriptive Statistics
- Exploratory Data Analysis (EDA)
- Correlation Analysis
- Trend Analysis
- Moving Average Analysis
- Volatility Analysis
- Monthly Trend Analysis



