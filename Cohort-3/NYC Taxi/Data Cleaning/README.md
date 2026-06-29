# NYC Yellow Taxi 2025 — Data Cleaning

**Project:** NYC Taxi Analysis
**Cohort:** Cohort-3
**Owner:** Saman
**Stage:** Data Cleaning 

---

## Dataset Download (Google Drive)

The raw and cleaned datasets are hosted on Google Drive due to their large size (~3 GB).

 **[Click here to download the dataset](https://drive.google.com/drive/folders/1dLu5APz_NJidr3ibMFmH1se2fF4uHrT0?usp=sharing)**

### What is inside the Drive folder

```
NYC_Taxi_Data/
├── rawData/                        ← Original files from NYC TLC website
│   ├── yellow_tripdata_2025-01.parquet
│   ├── yellow_tripdata_2025-02.parquet
│   ├── yellow_tripdata_2025-03.parquet
│   ├── yellow_tripdata_2025-04.parquet
│   ├── yellow_tripdata_2025-05.parquet
│   ├── yellow_tripdata_2025-06.parquet
│   ├── yellow_tripdata_2025-07.parquet
│   ├── yellow_tripdata_2025-08.parquet
│   ├── yellow_tripdata_2025-09.parquet
│   ├── yellow_tripdata_2025-10.parquet
│   ├── yellow_tripdata_2025-11.parquet
│   └── yellow_tripdata_2025-12.parquet
└── nyc_taxi_cleaned/               ← Cleaned output (ready for EDA & Tableau)
    ├── all_months_cleaned/         ← Full year, partitioned by month
    │   ├── pickup_month=1/
    │   ├── pickup_month=2/
    │   └── ... pickup_month=12/
    └── monthly_summary/            ← CSV summary for dashboards
```

### How to download

1. Click the Google Drive link above
2. Click the folder you need (`rawData` or `nyc_taxi_cleaned`)
3. Right-click → **Download**
4. Extract the zip file if downloaded as a folder
5. Place the files in your local project folder as shown in the folder structure above

---

## Data Source

- **Source:** NYC Taxi & Limousine Commission (TLC)
- **Website:** https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- **Dataset:** Yellow Taxi Trip Records — January to December 2025
- **Format:** Parquet files (one file per month)
- **Total raw rows:** ~42 million trips
- **Total raw size:** ~3 GB

### Raw Data Columns (20 columns)

| Column | Description |
|--------|-------------|
| VendorID | Taxi vendor (1 = Creative Mobile, 2 = VeriFone) |
| tpep_pickup_datetime | Trip pickup timestamp |
| tpep_dropoff_datetime | Trip dropoff timestamp |
| passenger_count | Number of passengers |
| trip_distance | Trip distance in miles |
| RatecodeID | Rate type (1=Standard, 2=JFK, 3=Newark, etc.) |
| store_and_fwd_flag | Whether trip was stored before sending to server |
| PULocationID | Pickup location zone ID (1–265) |
| DOLocationID | Dropoff location zone ID (1–265) |
| payment_type | Payment method (1=Credit Card, 2=Cash, etc.) |
| fare_amount | Base fare in USD |
| extra | Extra charges |
| mta_tax | MTA tax |
| tip_amount | Tip amount |
| tolls_amount | Tolls paid |
| improvement_surcharge | Improvement surcharge |
| total_amount | Total amount charged |
| congestion_surcharge | Congestion surcharge |
| Airport_fee | Airport fee |
| cbd_congestion_fee | CBD congestion fee (new for 2025) |

---

## Tools Used

- **Language:** Python 3
- **Framework:** PySpark 3.5.1 (chosen over Pandas due to 42M row dataset size)
- **Environment:** Jupyter Notebook
- **Storage:** Parquet format (columnar, compressed, fast to read)

---

## Data Cleaning Process

The cleaning was done in two phases.

---

### Phase 1 — One Month Deep Dive (January 2025)
**Script:** `nyc_taxi_phase1_one_month.ipynb`

Before cleaning all 12 months, January was cleaned first to fully understand the data — its schema, quality issues, and value ranges. Every decision made here was then applied to all 12 months in Phase 2.

---

### Phase 2 — All 12 Months Combined
**Script:** `nyc_taxi_phase2_all_months.ipynb`

The same cleaning logic was applied to all 12 files loaded together as one combined DataFrame.

---

## Cleaning Steps in Detail

### Step 1 — Raw Data Documentation
Before making any changes, the raw data was documented:
- Total row count and column count per file
- Schema (column names and data types)
- Missing value count and percentage for every column
- Unique values for categorical columns (VendorID, RatecodeID, payment_type)
- Date range of pickup timestamps
- Known data quality issues with exact counts

### Step 2 — Fix Data Types
Every column was cast to its correct type:
- ID columns → Integer (VendorID, RatecodeID, PULocationID, DOLocationID, payment_type, passenger_count)
- Timestamp columns → TimestampType (tpep_pickup_datetime, tpep_dropoff_datetime)
- Money and distance columns → Double (fare_amount, trip_distance, total_amount, etc.)
- Flag column → String (store_and_fwd_flag)

If a cast failed, the value became null — handled in the next step.

### Step 3 — Handle Missing Values

| Column | Strategy | Reason |
|--------|----------|--------|
| tpep_pickup/dropoff_datetime | Drop row | Trip with no timestamp is unusable |
| PULocationID / DOLocationID | Drop row | Trip with no location is unusable |
| congestion_surcharge, Airport_fee, cbd_congestion_fee, extra, mta_tax, tip_amount, tolls_amount, improvement_surcharge | Fill → 0.0 | Vendor 6 & 7 don't report surcharges — absence means $0 |
| passenger_count | Fill → 1 | Most common value; null pattern matches vendor 6/7 |
| VendorID / RatecodeID | Fill → -1 | Sentinel value meaning "Unknown" |
| payment_type = 0 | Recode → -1 | Code 0 = Unknown, standardised to -1 |
| store_and_fwd_flag | Fill → 'N' | Not forwarded is the default |

### Step 4 — Remove Duplicates
Duplicate rows were detected using 7 key business columns:
- VendorID, tpep_pickup_datetime, tpep_dropoff_datetime
- PULocationID, DOLocationID, fare_amount, total_amount

Any row where all 7 columns matched an existing row was dropped.

### Step 5 — Validate and Filter Bad Data
The following rules were applied and each one's row removal count was logged:

| Rule | Condition |
|------|-----------|
| Pickup before dropoff | pickup_datetime < dropoff_datetime |
| Valid year | Pickup date within 2025 |
| Each row matches its source file month | date_format(pickup) == source_month |
| Trip duration | 1 minute to 24 hours |
| Trip distance | Greater than 0, less than 500 miles |
| Fare amount | $0 to $50,000 |
| Total amount | Greater than or equal to $0 |
| Airport fee | Greater than or equal to $0 |
| CBD congestion fee | Greater than or equal to $0 |
| Passenger count | 1 to 9 (NYC TLC maximum) |
| RatecodeID = 99 | Recoded to -1 (Unknown) |

### Step 6 — Add Derived Columns
These columns were computed once during cleaning to save time in EDA:

| New Column | Description |
|------------|-------------|
| pickup_date | Date portion of pickup timestamp |
| pickup_year | Year of pickup |
| pickup_month | Month number (1–12) |
| pickup_day | Day of month |
| pickup_hour | Hour of pickup (0–23) |
| pickup_dayofweek | Day of week (1=Sun, 7=Sat) |
| pickup_dayname | Day name (Monday, Tuesday, etc.) |
| is_weekend | True if Saturday or Sunday |
| time_of_day | Morning / Afternoon / Evening / Night / Late Night |
| trip_duration_minutes | Dropoff minus pickup in minutes |
| avg_speed_mph | trip_distance divided by duration in hours |
| fare_per_mile | fare_amount divided by trip_distance |
| tip_pct | tip_amount as percentage of fare_amount |
| payment_label | Human-readable payment type label |
| ratecode_label | Human-readable rate code label |

---

## Cleaning Results Summary

| Metric | Value |
|--------|-------|
| Raw rows (all 12 months) | ~42,000,000 |
| Cleaned rows | ~38,500,000 |
| Rows removed | ~3,500,000 (~8%) |
| Data retained | ~92% |
| Final columns | 31 (20 original + 11 derived) |
| Output format | Parquet, partitioned by pickup_month |

---

## Scripts in this Folder

| File | Purpose |
|------|---------|
| `nyc_taxi_phase1_one_month.ipynb` | Phase 1 — Clean and analyse January 2025 only |
| `nyc_taxi_phase2_all_months.ipynb` | Phase 2 — Clean all 12 months combined and export |

---

## How to Run the Scripts

### Requirements
```
Python 3.10+
pyspark==3.5.1
pyarrow
pandas
numpy
jupyter
```

### Install
```bash
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install pyspark==3.5.1 pyarrow pandas numpy jupyter
```

### Run
1. Download the dataset from the Google Drive link above
2. Place the 12 parquet files in `NYC_Data/rawData/`
3. Open Jupyter: `jupyter notebook`
4. Run Phase 1 first, then Phase 2

---

## ✅ Checklist

- [x] Raw data loaded and documented (source, rows, columns)
- [x] Missing values and duplicates handled
- [x] Data types corrected and validated
- [x] Clean dataset exported for the team
- [x] Cleaning steps explained in this README
