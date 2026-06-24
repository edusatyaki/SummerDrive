# A-B Test - Data Cleaning

**Cohort:** Cohort-3  
**Owner:** Farhana

## Purpose
Load the raw dataset, handle missing values, fix data types, remove duplicates, and export a clean dataset the rest of the team can use.

## Checklist
- [x] Raw data loaded and documented (source, rows, columns)
- [x] Missing values and duplicates handled
- [x] Data types corrected and validated
- [x] Clean dataset exported for the team
- [x] Cleaning steps explained in this README

## Cleaning and Engineering Steps
1. **Raw Data Load**: Loaded `marketing_AB.csv` consisting of 588,101 rows and 7 columns.
2. **Standardization**: Stripped and converted all column names to lowercase snake_case (e.g., `user_id`, `test_group`, `total_ads`, `most_ads_day`, `most_ads_hour`).
3. **Data Type Correction**: Created a `converted_int` column from `converted` (mapping True/False to 1/0).
4. **Feature Engineering**:
   - Added `is_weekend` (1 if `most_ads_day` is Saturday or Sunday, else 0).
   - Added `hour_period` (mapping hours to 'morning', 'afternoon', 'evening', or 'night').
   - Added `ads_bucket` (binned total ads into quantiles: 'low', 'medium', 'high', 'very_high').
5. **Output**: Saved the engineered and cleaned dataset as `marketing_AB_engineered.csv` for the A-B test analysis.

## Files in this folder
- `ABtest.ipynb`: Jupyter Notebook detailing the data cleaning and feature engineering process.
- `marketing_AB_engineered.csv`: The cleaned and engineered dataset.
