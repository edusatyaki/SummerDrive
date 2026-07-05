# 🩺 Diabetes 130-US Hospitals Data Cleaning Project

## Project Overview

This project focuses on cleaning and preprocessing the **Diabetes 130-US Hospitals for Years 1999–2008** dataset obtained from the UCI Machine Learning Repository. The goal is to transform the raw healthcare dataset into a clean, structured, and machine-learning-ready dataset by handling missing values, encoding categorical features, validating data, and optimizing memory usage. :contentReference[oaicite:0]{index=0}

---

##  Dataset Information

- **Dataset Name:** Diabetes 130-US Hospitals for Years 1999–2008
- **Source:** UCI Machine Learning Repository
- **Rows:** 101,766
- **Columns:** 50
- **Dataset Type:** Real-world Healthcare Dataset :contentReference[oaicite:1]{index=1}

---

##  Project Objectives

- Understand the dataset structure
- Identify missing values
- Clean inconsistent data
- Handle categorical variables
- Encode features for machine learning
- Remove duplicate records
- Validate numerical ranges
- Optimize memory usage
- Generate cleaning logs
- Export the cleaned dataset

---

##  Technologies Used

- Python
- Pandas
- NumPy
- Google Colab / Jupyter Notebook

---

## 📁 Project Structure

```
├── diabetes_cleaning.ipynb
├── Cleaned_Dataset/
│   ├── diabetes_cleaned_dataset.csv
│   ├── diabetes_cleaned_dataset.parquet
│   ├── diabetes_cleaning_log.csv
│   └── diabetes_final_summary.csv
└── README.md
```

---

##  Data Cleaning Steps

### 1. Dataset Loading

- Loaded the raw CSV dataset
- Performed initial inspection
- Checked dataset dimensions
- Viewed column names and data types

### 2. Missing Value Handling

- Converted "?" into NaN
- Filled missing values using mode where appropriate
- Removed columns with excessive missing values:
  - weight
  - payer_code
  - medical_specialty

### 3. Feature Cleaning

- Converted categorical variables into numerical values
- Removed invalid gender values
- Converted age groups into representative numerical ages
- Handled diagnosis columns
- Encoded medicine-related columns
- Encoded laboratory result columns

### 4. Target Variable Encoding

Mapped:

- NO → 0
- >30 → 1
- <30 → 2

### 5. Duplicate Removal

- Removed duplicate hospital encounters using encounter_id.

### 6. Data Validation

Validated important numerical columns including:

- time_in_hospital
- num_lab_procedures
- num_medications
- number_outpatient
- number_emergency
- number_inpatient
- number_diagnoses

### 7. Memory Optimization

- Downcast numeric columns
- Converted suitable object columns into category dtype
- Reduced overall memory consumption

### 8. Final Validation

Performed final checks for:

- Missing values
- Duplicate rows
- Data types
- Dataset shape
- Memory usage

---

## 📈 Output Files

The notebook generates:

- ✅ Cleaned Dataset (CSV)
- ✅ Cleaned Dataset (Parquet)
- ✅ Cleaning Log
- ✅ Final Summary Report

---


4. Run all notebook cells.

---

##  Key Features

- Complete data cleaning pipeline
- Missing value handling
- Feature engineering
- Data validation
- Machine Learning ready dataset
- Memory optimization
- Automatic cleaning log generation
- Export in CSV and Parquet formats

---

## Dataset Source

UCI Machine Learning Repository

Dataset:
Diabetes 130-US Hospitals for Years 1999–2008

---

##  Author

**Drishti**

---
