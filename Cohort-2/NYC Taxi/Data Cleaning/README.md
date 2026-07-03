# 🧹 NYC Yellow Taxi 2025 – Data Cleaning

## 📌 Overview

This folder contains the complete data cleaning process for the **NYC Yellow Taxi 2025** dataset using **PySpark**.

The goal of this phase is to improve data quality by removing duplicate records, handling missing values, validating business rules, correcting data types, and eliminating invalid records. The cleaned dataset is prepared for further analysis and visualization.

---

# 📂 Folder Structure

```
Data Cleaning/
│
├── Raw Dataset/
│   ├── Original monthly Parquet files
│
├── Cleaned Dataset/
│   ├── NYC_Taxi_Cleaning.ipynb
│   ├── Cleaned Parquet Dataset
│
└── README.md
```

---

# 📖 Data Cleaning Workflow

The following steps were performed during data cleaning:

1. Load and merge all monthly datasets.
2. Understand the dataset structure.
3. Check missing values and duplicate records.
4. Convert columns to appropriate data types.
5. Handle missing values.
6. Validate important business columns.
7. Remove invalid records.
8. Verify the cleaned dataset.
9. Save the cleaned dataset.

---

# 🛠 Cleaning Tasks Performed

- ✅ Duplicate record removal
- ✅ Data type conversion
- ✅ Missing value handling
- ✅ RatecodeID cleaning
- ✅ Store & Forward Flag cleaning
- ✅ Passenger Count validation
- ✅ Trip Distance validation
- ✅ Fare Amount validation
- ✅ Total Amount validation
- ✅ Pickup & Drop-off Datetime validation
- ✅ Final data quality verification

---

# 📁 Raw Dataset

The **Raw Dataset** folder contains the original NYC Yellow Taxi monthly Parquet files without any modifications. These files are used as the source for the data cleaning process.

---

# 📁 Cleaned Dataset

The **Cleaned Dataset** folder contains:

- Data cleaning notebook (`.ipynb`)
- Cleaned Parquet dataset

The cleaned dataset has:

- Duplicate records removed
- Missing values handled
- Invalid records removed
- Correct data types applied
- Business rules validated

---

# 📊 Output

The final cleaned dataset is ready for:

- Exploratory Data Analysis (EDA)
- Statistical Analysis
- Tableau Dashboard Development
- Further data analytics
