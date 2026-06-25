# Cleaning Log

## Project: Diabetes Dataset Cleaning

### Overview

This document records the data cleaning steps performed on the Diabetes Dataset before analysis and machine learning. The objective is to improve the quality of the dataset by handling missing values, removing unnecessary data, and preparing the dataset for further use.

---

## Cleaning Steps

### 1. Load the Dataset

**Purpose:**
Load the diabetes dataset into a pandas DataFrame.

**Result:**
The dataset is successfully loaded and ready for preprocessing.

---

### 2. Replace Missing Value Symbols

**Action:**
Replaced all `"?"` values with `NaN`.

**Why?**
The dataset uses `"?"` to represent missing values. Converting them to `NaN` allows pandas to recognize and handle missing data correctly.

**Result:**
All missing values are stored in a standard format.

---

### 3. Check Missing Values

**Action:**
Checked the number of missing values in each column.

**Why?**
To identify which columns contain missing data before cleaning.

**Result:**
Missing values were identified for further processing.

---

### 4. Remove Unnecessary Columns

**Columns Removed:**

* weight
* payer_code
* medical_specialty

**Why?**
These columns contained a large number of missing values and were not required for this project.

**Result:**
The dataset became smaller and easier to work with.

---

### 5. Remove Rows with Missing Values

**Action:**
Removed rows containing remaining missing values.

**Why?**
Incomplete records may affect analysis and machine learning model performance.

**Result:**
Only complete records remain in the dataset.

---

### 6. Convert Age Ranges to Numeric Values

**Action:**
Converted age ranges (for example, `[50-60)`) into approximate numerical values (such as `55`).

**Why?**
Numeric values are easier to analyze and can be used directly in machine learning models.

**Result:**
The age column now contains numerical values.

---

### 7. Remove Invalid Gender Records

**Action:**
Removed rows where the gender value was `"Unknown/Invalid"`.

**Why?**
Invalid entries may reduce the quality and accuracy of analysis.

**Result:**
Only valid gender records remain.

---

### 8. Save the Cleaned Dataset

**Action:**
Saved the cleaned dataset as a CSV file.

**Result:**
The cleaned dataset is stored in the `cleaned_data` folder and is ready for analysis or machine learning.

---

# Final Outcome

After completing the cleaning process:

* Missing values were handled.
* Unnecessary columns were removed.
* Incomplete records were removed.
* Age values were converted into numeric format.
* Invalid gender records were removed.
* The cleaned dataset was successfully saved.

The final dataset is cleaner, more consistent, and ready for data analysis and machine learning applications.

