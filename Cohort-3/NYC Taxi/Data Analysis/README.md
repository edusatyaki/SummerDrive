# NYC Yellow Taxi 2025 — Demand & Pricing Analytics

**Project:** NYC Taxi Analysis
**Cohort:** Cohort-3
**Owner:** Farhana
**Stage:** Data Analysis — Phase 2

---

## Data Source

- **Source:** Saman's cleaned dataset (Phase 1 & 2 cleaning)
- **Dataset:** NYC Yellow Taxi Trip Records — January to December 2025
- **Format:** Parquet, partitioned by pickup_month
- **Total rows:** 43,790,431 (after cleaning)
- **Total columns:** 35 (20 original + 15 derived)

---

## Tools Used

- **Language:** Python 3
- **Framework:** PySpark 4.0.3
- **Environment:** Google Colab
- **Visualisation:** Matplotlib, Seaborn

---

## How to Access the Data

The cleaned dataset is hosted on Google Drive by Saman.

**[Click here to access the dataset](https://drive.google.com/drive/folders/1dLu5APz_NJidr3ibMFmH1se2fF4uHrT0?usp=sharing)**

Load it in your notebook:
```python
from google.colab import drive
drive.mount('/content/drive')

DRIVE_PATH = "/content/drive/.shortcut-targets-by-id/1AG7n5J82rGTCKZTIhAWnWDJ0Ia16Ugcb/all_months_cleaned"
df = spark.read.parquet(DRIVE_PATH)
```

---

## Analysis Tasks

### Task 1 — Monthly Trip Volume & Revenue Seasonality
- Grouped all trips by month
- Counted total trips and summed total revenue per month
- Identified peak and low demand months across 2025
- **Output:** `monthly_seasonality.png`

### Task 2 — Hourly Demand Heatmap (Weekday vs Weekend)
- Grouped trips by hour of day and weekend/weekday flag
- Built a heatmap showing demand intensity across all 24 hours
- Identified peak hours for weekdays vs weekends separately
- **Output:** `hourly_demand_heatmap.png`

### Task 3 — Fare Distribution & Airport vs Standard Trip Economics
- Filtered trips to Standard, JFK, and Newark rate types
- Compared avg fare, avg distance, avg tip %, and fare per mile
- Plotted fare distribution histograms for each trip type
- **Output:** `fare_distribution.png`

### Task 4 — Tip Rate Analysis by Hour (Late Night Premium)
- Filtered to credit card trips only (cash tips not recorded by TLC)
- Computed avg tip % and avg tip amount for each hour of the day
- Measured late night (12AM–4AM) tip premium vs overall average
- **Output:** `tip_rate_analysis.png`

### Task 5 — CBD Congestion Fee Impact ($0.75 Fee) Behavioral Shifts
- Split trips into "With CBD Fee" vs "No CBD Fee" groups
- Compared avg fare, avg total, avg distance, avg tip %, avg passengers
- Plotted % of trips with CBD fee by hour of day
- **Output:** `cbd_fee_impact.png`

### Task 6 — Driver Revenue Optimization Model (Best Shifts)
- Defined 3 shifts: Morning (6AM–2PM), Afternoon (2PM–10PM), Night (10PM–6AM)
- Split each shift by weekday vs weekend
- Compared avg revenue per trip and avg tip % across all 6 combinations
- Identified the most profitable shift for drivers
- **Output:** `driver_revenue_optimization.png`

---

## Output Files

| File | Description |
|------|-------------|
| `nyc_taxi_demand_pricing.ipynb` | Full analysis notebook |
| `monthly_seasonality.png` | Task 1 — Monthly trip volume & revenue charts |
| `hourly_demand_heatmap.png` | Task 2 — Hourly demand heatmap |
| `fare_distribution.png` | Task 3 — Fare distribution & airport economics |
| `tip_rate_analysis.png` | Task 4 — Tip rate by hour |
| `cbd_fee_impact.png` | Task 5 — CBD congestion fee impact |
| `driver_revenue_optimization.png` | Task 6 — Driver revenue optimization |

---

## How to Run

### Requirements
- Python 3.10+
- pyspark
- pandas
- matplotlib
- seaborn
### Install
```bash
pip install pyspark pandas matplotlib seaborn
```

### Run
1. Open `nyc_taxi_demand_pricing.ipynb` in Google Colab
2. Mount your Google Drive and add Saman's dataset shortcut
3. Runtime → Run All

---

## Checklist

- [x] Monthly trip volume & revenue seasonality charts
- [x] Hourly demand heatmap (weekday vs weekend)
- [x] Fare distribution & airport vs standard trip economics
- [x] Tip rate analysis by hour (late night premium)
- [x] CBD Congestion Fee impact behavioral shifts
- [x] Driver revenue optimization model (best shifts)