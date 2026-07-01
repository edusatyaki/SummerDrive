# Marketing A/B Test — Data Cleaning

**Project:** A/B Test Analysis  
**Cohort:** Cohort-3  
**Owner:** Farhana  
**Stage:** Data Cleaning  

---

## Data Source

- **Source:** Kaggle — Marketing A/B Testing Dataset
- **Link:** https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing
- **Dataset size:** 588,101 rows, 7 columns
- **Format:** CSV

### Raw Columns

| Column | Description |
|--------|-------------|
| Unnamed: 0 | Auto-generated row index from CSV export — not useful |
| user id | Unique identifier for each user |
| test group | Whether the user was shown an ad or a PSA |
| converted | Whether the user converted (True/False) |
| total ads | Total number of ads shown to the user |
| most ads day | Day of the week when the user saw the most ads |
| most ads hour | Hour of the day when the user saw the most ads (0–23) |

---

## Tools Used

- **Language:** Python 3
- **Libraries:** pandas, numpy
- **Environment:** Google Colab

---

## Cleaning Steps

### Step 1 — Document the Raw Data

Before touching anything, I recorded the state of the raw data:
- Shape, column types, and basic info
- Missing value counts per column
- Number of duplicate rows
- Numeric and categorical summary statistics
- Group split between ad and psa users

This gives a baseline to compare against after cleaning.

### Step 2 — Drop Redundant Column and Rename

- Dropped `Unnamed: 0` — it is just a row counter from the CSV export and carries no real information
- Renamed all columns to snake_case (e.g. `user id` became `user_id`) for consistency and easier handling in code

### Step 3 — Handle Missing Values and Duplicates

| Column | Issue | Fix |
|--------|-------|-----|
| Unnamed: 0 | Redundant index column | Dropped entirely |
| user_id | No issues | Kept as-is |
| test_group | No issues | Kept as-is |
| converted | Boolean (True/False) | Converted to integer (0/1) as `converted_int` |
| total_ads | Heavily right-skewed, max value 2065 | Bucketed into categories using `pd.qcut` |
| most_ads_day | No issues | Used to derive `is_weekend` |
| most_ads_hour | No issues | Used to derive `hour_period` |

No rows were dropped. The dataset had no missing values or duplicate rows to begin with.

### Step 4 — Feature Engineering

Four new columns were added to make the data more useful for analysis:

| New Column | Description |
|------------|-------------|
| converted_int | The `converted` boolean mapped to 1 (True) or 0 (False) |
| is_weekend | 1 if the user saw the most ads on Saturday or Sunday, else 0 |
| hour_period | Hour grouped into morning, afternoon, evening, or night (ordered category) |
| ads_bucket | Total ads bucketed into low, medium, high, or very_high quartiles |

### Step 5 — Data Type Optimization

Column types were tightened to reduce memory usage:
- `test_group`, `most_ads_day`, `hour_period` converted to `category`
- `converted_int`, `is_weekend`, `most_ads_hour` converted to `int8`
- `total_ads` downcasted to the smallest fitting integer type

Memory dropped from about 80 MB to around 10 MB — an 87% reduction.

### Step 6 — Final Check

- Confirmed 0 nulls across all columns
- Confirmed 0 duplicate rows
- Verified final dtypes
- Exported cleaned dataset as `marketing_AB_cleaned.csv`

---

## Results Summary

| Metric | Value |
|--------|-------|
| Raw rows | 588,101 |
| Cleaned rows | 588,101 |
| Rows removed | 0 |
| Original columns | 7 |
| Final columns | 10 |
| Memory before | ~80 MB |
| Memory after | ~10 MB |
| Output format | CSV |

---

## Group Split

| Group | Count | Percentage |
|-------|-------|------------|
| ad | 564,577 | 96% |
| psa | 23,524 | 4% |

---

## Files in This Folder

| File | Description |
|------|-------------|
| `AB_test_data_cleaning.ipynb` | Notebook with all cleaning and feature engineering steps |
| `marketing_AB.csv` | Original raw dataset from Kaggle |
| `marketing_AB_cleaned.csv` | Cleaned and engineered dataset ready for analysis |

---

## How to Run

**Requirements:**
- Python 3.10 or above
- pandas
- numpy

**Install dependencies:**
```bash
pip install pandas numpy
```

**Steps:**
1. Upload `marketing_AB.csv` to your Colab session
2. Open `AB_test_data_cleaning.ipynb`
3. Go to Runtime and click Run All

---

## Checklist

- Raw data loaded and documented
- Missing values and duplicates checked
- Data types corrected and optimised
- Feature engineering completed
- Cleaned dataset exported for the team
- Cleaning steps explained in this README