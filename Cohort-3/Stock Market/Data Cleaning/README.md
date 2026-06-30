# 📈 Market Time Series Forecasting — Data Cleaning

**Project:** Market Time Series Forecasting
**Dataset:** Yahoo Finance Historical Stock Data
**Owner:** Akshat Agrawal
**Stage:** Data Cleaning

---

# Dataset

Historical stock market data was collected directly from Yahoo Finance using the `yfinance` Python library.

## Stocks Used

* AAPL (Apple Inc.)
* MSFT (Microsoft Corporation)
* SPY (SPDR S&P 500 ETF Trust)

## Time Period

Approximately **5 years** of daily historical trading data.

## Data Source

* **Source:** Yahoo Finance
* **Library:** `yfinance`
* **Frequency:** Daily
* **Format:** CSV (exported after download)

---

# Project Structure

```text
Market_Time_Series_Forecasting/
│
├── README.md
├── Cleaned_Data_Stock_Marketing.ipynb
├── raw_stock_data.csv
└── clean_stock_data.csv
```

---

# Dataset Description

The dataset contains historical daily OHLCV (Open, High, Low, Close, Volume) market data.

### Original Columns

| Column | Description                                      |
| ------ | ------------------------------------------------ |
| Open   | Opening price                                    |
| High   | Highest trading price                            |
| Low    | Lowest trading price                             |
| Close  | Closing price (adjusted when `auto_adjust=True`) |
| Volume | Number of shares traded                          |

The dataset was collected for three securities:

* AAPL
* MSFT
* SPY

The downloaded data uses a **MultiIndex column structure**, where each OHLCV field contains values for all three securities.

---

# Tools Used

* Python 3
* Google Colab
* Pandas
* NumPy
* yfinance

---

# Data Cleaning Process

The cleaning workflow consisted of four major steps.

---

## Step 1 — Data Collection & Initial Inspection

Historical stock prices were downloaded using the `yfinance` library.

Immediately after downloading, the original dataset was exported as:

```
raw_stock_data.csv
```

The following checks were performed before cleaning:

* Dataset dimensions (`shape`)
* First five rows (`head()`)
* Data types (`info()`)
* Summary statistics (`describe()`)
* Missing values (`isnull().sum()`)
* Duplicate records (`duplicated().sum()`)

### Objective

* Understand the dataset structure.
* Verify column names and data types.
* Detect missing values.
* Detect duplicate records.

---

## Step 2 — Handle Non-Trading Days & Missing Data

The dataset was inspected for missing values and non-trading day gaps.

### Observations

* The downloaded dataset contains only trading days.
* Weekends and market holidays are naturally excluded by Yahoo Finance.
* No unexpected missing values were detected.
* No duplicate records were found.

### Cleaning Decision

* No rows were removed.
* No missing values required imputation.
* No forward-filling was applied.
* The original trading-day calendar was retained.

---

## Step 3 — Data Type Validation & Memory Optimization

The dataset was validated to ensure:

* Correct numeric data types.
* Proper `DatetimeIndex`.
* Consistent MultiIndex column structure.

To improve memory efficiency:

* Price columns were converted from `float64` to `float32`.
* Volume columns were converted from `int64` to `int32`.

Memory usage was compared before and after optimization.

---

## Step 4 — Final Validation & Export

After completing the cleaning process, the dataset was validated using:

* `info()`
* `isnull().sum()`
* `duplicated().sum()`

The cleaned dataset was exported as:

```
clean_stock_data.csv
```

---

# Cleaning Summary

| Check                      | Status |
| -------------------------- | ------ |
| Raw dataset downloaded     | ✅      |
| Raw dataset exported       | ✅      |
| Dataset inspected          | ✅      |
| Missing values checked     | ✅      |
| Duplicate records checked  | ✅      |
| Data types validated       | ✅      |
| Memory optimized           | ✅      |
| Final validation completed | ✅      |
| Clean dataset exported     | ✅      |

---

# Files Included

| File                                 | Description                                                                                                           |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| `Cleaned_Data_Stock_Marketing.ipynb` | Google Colab notebook containing the complete data collection, inspection, cleaning, validation, and export workflow. |
| `raw_stock_data.csv`                 | Original historical stock market dataset downloaded from Yahoo Finance.                                               |
| `clean_stock_data.csv`               | Final cleaned dataset after preprocessing and validation.                                                             |
| `README.md`                          | Documentation describing the dataset, data cleaning workflow, and project structure.                                  |

---

# Requirements

```text
Python 3.10+

pandas
numpy
yfinance
```

Install dependencies:

```bash
pip install pandas numpy yfinance
```

---

# How to Run

1. Clone or download this repository.
2. Open `Cleaned_Data_Stock_Marketing.ipynb` using **Google Colab**.
3. Install the required libraries if needed.
4. Run all notebook cells sequentially.
5. The notebook will:

   * Download historical stock data from Yahoo Finance.
   * Export `raw_stock_data.csv`.
   * Inspect and validate the dataset.
   * Perform data cleaning and memory optimization.
   * Export `clean_stock_data.csv`.

---

# Workflow

```text
Download Historical Stock Data
            │
            ▼
Export Raw Dataset
            │
            ▼
Initial Data Inspection
            │
            ▼
Missing Value Analysis
            │
            ▼
Duplicate Record Check
            │
            ▼
Data Type Validation
            │
            ▼
Memory Optimization
            │
            ▼
Final Validation
            │
            ▼
Export Clean Dataset
```

---

# Deliverables

* ✅ Historical stock market data downloaded from Yahoo Finance
* ✅ Raw dataset exported for reproducibility
* ✅ Dataset inspected and documented
* ✅ Missing values and duplicate records verified
* ✅ Data types validated
* ✅ Memory usage optimized
* ✅ Final cleaned dataset exported
* ✅ Complete Google Colab notebook included
