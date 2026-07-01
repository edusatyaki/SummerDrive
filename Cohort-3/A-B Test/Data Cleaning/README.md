# Marketing A/B Test — Data Cleaning

**Project:** A/B Test Analysis
**Cohort:** Cohort-3
**Owner:** Farhana
**Stage:** Data Cleaning

---

## Data Source

- **Source:** Kaggle — Marketing A/B Testing Dataset
- **Website:** https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing
- **Dataset:** Marketing A/B Test — 588,101 users
- **Format:** CSV (1 file)
- **Total raw rows:** 588,101
- **Total raw columns:** 7

### Raw Data Columns (7 columns)

| Column | Description |
|--------|-------------|
| Unnamed: 0 | CSV row-index artifact — not real data |
| user id | Unique identifier per user |
| test group | Whether user saw 'ad' or 'psa' |
| converted | Whether user converted (True/False) |
| total ads | Number of ads shown to the user |
| most ads day | Day of week user saw the most ads |
| most ads hour | Hour of day user saw the most ads (0–23) |

---

## Tools Used

- **Language:** Python 3
- **Libraries:** pandas, numpy
- **Environment:** Google Colab

---

## Cleaning Steps in Detail

### Step 1 — Raw Data Documentation
Before making any changes, the raw data was documented:
- Shape, dtypes, and info
- Missing value count per column
- Duplicate row count
- Numeric and categorical summary statistics
- Group split validation (ad vs psa)

### Step 2 — Drop Redundant Column & Rename
- Dropped `Unnamed: 0` — CSV index artifact, adds no value
- Renamed all columns to snake_case for consistency

### Step 3 — Handle Missing Values & Duplicates

| Column | Issue Found | Fix Applied |
|--------|-------------|-------------|
| Unnamed: 0 | Redundant index | Dropped |
| user_id | None | Kept as-is |
| test_group | None | Kept as-is |
| converted | Boolean dtype | Converted to converted_int (0/1) |
| total_ads | Heavily right-skewed (max 2065) | Bucketed safely with duplicates='drop' |
| most_ads_day | None | Used to derive is_weekend |
| most_ads_hour | None | Used to derive hour_period |

### Step 4 — Feature Engineering

| New Column | Description |
|------------|-------------|
| converted_int | Boolean converted → integer (0/1) |
| is_weekend | 1 if most_ads_day is Saturday or Sunday, else 0 |
| hour_period | morning / afternoon / evening / night (ordered category) |
| ads_bucket | total_ads bucketed into low / medium / high / very_high |

### Step 5 — Dtype Optimization & Memory Reduction
- `test_group`, `most_ads_day`, `hour_period` → category
- `converted_int`, `is_weekend`, `most_ads_hour` → int8
- `total_ads` → downcasted integer
- Memory usage measured before and after

### Step 6 — Final Verification
- Confirmed 0 nulls, 0 duplicates in cleaned dataset
- Final dtypes verified
- Cleaned dataset exported as CSV

---

## Cleaning Results Summary

| Metric | Value |
|--------|-------|
| Raw rows | 588,101 |
| Cleaned rows | 588,101 |
| Rows removed | 0 |
| Original columns | 7 |
| Final columns | 10 (7 original + 3 engineered, 1 dropped) |
| Output format | CSV |

---

## Group Split Validation

| Group | Count | Percentage |
|-------|-------|------------|
| ad | ~564,577 | ~96% |
| psa | ~23,524 | ~4% |

---

## Scripts in this Folder

| File | Purpose |
|------|---------|
| `AB_test_data_cleaning.ipynb` | Full cleaning notebook |
| `marketing_AB_cleaned.csv` | Cleaned dataset for team use |

---

## How to Run

### Requirements
- Python 3.10+
- pandas
- numpy

### Install
```bash
pip install pandas numpy
```

### Run
1. Upload `marketing_AB.csv` to your Colab session
2. Open `AB_test_data_cleaning.ipynb`
3. Runtime → Run All

---

## ✅ Checklist

- [x] Raw data loaded and documented (source, rows, columns)
- [x] Missing values and duplicates handled
- [x] Data types corrected and validated
- [x] Clean dataset exported for the team
- [x] Cleaning steps explained in this README