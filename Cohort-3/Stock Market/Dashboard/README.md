# Stock Market Forecasting — Dashboard & Reporting

**Project:** Stock Market Analysis — AAPL / MSFT / SPY
**Cohort:** Cohort-3
**Owner:** Farhana
**Stage:** Phase 4 — Dashboard & Reporting

---

## Overview

This phase builds on Akshat's financial EDA (Phase 0–2) and Saman's forecasting models (Phase 3) to deliver an interactive Tableau dashboard, a BI data export pipeline, and an executive summary on forecast reliability.

---

## Data Sources

| File | Source | Purpose |
|------|--------|---------|
| `cleaned_stock_data.csv` | Akshat — Data Cleaning | Raw cleaned OHLCV data for AAPL, MSFT, SPY |
| `stock_historical_for_BI.csv` | Exported by this phase | Price, indicators, Bollinger Bands per ticker |
| `stock_returns_for_BI.csv` | Exported by this phase | Daily returns for all three tickers side by side |
| `stock_monthly_summary_for_BI.csv` | Exported by this phase | Monthly return aggregates for seasonality analysis |

---

## Tools Used

- **Language:** Python 3
- **Environment:** Google Colab
- **Dashboard:** Tableau Desktop (.twbx)
- **Libraries:** pandas, numpy

---

## Phase 4 Tasks

### Task 1 — Export Predictions and Historical Data for BI

**Notebook:** `stock_market_dashboard_export.ipynb`

The cleaned stock dataset was loaded from GitHub, processed, and exported as three BI-ready CSV files.

**Step 1 — Load & flatten MultiIndex columns**
The raw `cleaned_stock_data.csv` uses a two-level MultiIndex column structure (metric, ticker). The notebook flattened this into single-level columns like `Close_AAPL`, `Open_MSFT` etc., then separated the data into per-ticker DataFrames.

**Step 2 — Add technical indicators**
For each ticker (AAPL, MSFT, SPY), the following indicators were computed:
- `SMA_50` — 50-day Simple Moving Average
- `SMA_200` — 200-day Simple Moving Average
- `EMA_50` — 50-day Exponential Moving Average
- `Daily_Return` — daily percentage change in Close price
- `Cumulative_Return` — compounded return from start date
- `Volatility_20d` — 20-day rolling standard deviation of returns
- `BB_Upper`, `BB_Mid`, `BB_Lower` — Bollinger Bands (20-day, ±2 std dev)

**Step 3 — Export three BI-ready CSVs**

| File | Contents | Rows |
|------|----------|------|
| `stock_historical_for_BI.csv` | Daily OHLCV + all indicators, all tickers stacked | ~3,762 |
| `stock_returns_for_BI.csv` | Daily returns for AAPL, MSFT, SPY in wide format | ~1,254 |
| `stock_monthly_summary_for_BI.csv` | Monthly aggregated returns per ticker | ~180 |

---

### Task 2 — Build Interactive Financial Dashboard (Tableau)

An 11-sheet Tableau workbook covering price analysis, volume, technical indicators, returns, correlation, and seasonality, organized into 3 summary dashboard views.

#### Individual Sheets

| Sheet | Chart Type | Description |
|-------|-----------|-------------|
| Price Overview | Dual-axis line chart | Close price + 50/200-day moving averages for AAPL, MSFT, SPY |
| Volume | Small multiples bar chart | Trading volume over time for each ticker separately |
| Bollinger Bands | Line chart | BB Upper, BB Mid, BB Lower and Close for selected ticker |
| Volatility | Area chart | 20-day rolling volatility — highlights volatility clustering |
| Returns Comparison | Bar chart | Daily returns for AAPL, MSFT, SPY side by side |
| Correlation | Scatter plot | AAPL vs SPY daily returns — beta = 1.195, p < 0.0001 |
| Correlation MSFT | Scatter plot | MSFT vs SPY daily returns — beta = 1.115, p < 0.0001 |
| Seasonality | Grouped bar chart | Monthly returns for all three tickers across full 5-year window |

#### Dashboard Views

**Trading Desk View — "How is the stock behaving right now?"**
Combines Price & Moving Averages, Bollinger Bands, Volume, and 20-Day Volatility. Includes written insights covering trend direction, golden/death cross signals, volatility clustering, and volume spikes.

**Portfolio Risk View — "How do these stocks move together?"**
Combines Daily Returns comparison with AAPL vs SPY and MSFT vs SPY scatter plots. Includes written insights on beta interpretation, diversification implications, and statistical significance of correlations.

**Strategy Planning View — "Are there seasonal patterns worth planning around?"**
Monthly returns bar chart across the full 5-year window with written insights covering AAPL's strongest month (July, +0.307% avg daily return), weakest month (September, −0.162%), and a caution that these are descriptive patterns over a limited window, not reliable trading signals.

---

### Task 3 — Executive Summary on Forecast Reliability

#### Model Performance (from Saman's Phase 3 forecasting)

| Model | RMSE | MAPE | Verdict |
|-------|------|------|---------|
| SARIMA (0,1,2) | ~9.7 | ~2.6% | Best performer on 30-day holdout |
| Facebook Prophet | ~23.1 | ~6.9% | Underperformed due to sharp price movement in test window |

#### Key Findings

- The AAPL price series is non-stationary in level but stationary after first differencing of log returns, confirming ARIMA family models are appropriate
- SARIMA outperformed Prophet significantly — RMSE was roughly 2.4x lower on the 30-day test window
- Prophet's underperformance is explained by a sharp short-term price movement in the evaluation window — Prophet's trend component smooths over sudden moves rather than tracking them
- Both models produce widening confidence intervals beyond 2 weeks, meaning short-term forecasts are more reliable than longer-horizon ones
- Neither model should be used for trading decisions in isolation

#### Recommendation
SARIMA(0,1,2) is the preferred model for short-term AAPL price forecasting on this dataset. For production use, the model should be retrained monthly on a rolling window and evaluated against a fresh holdout set each time.

---

### Task 4 — Publish GitHub Repository
All files committed to `Cohort-3 → Stock Market → Dashboard`.

---

## Files in this Folder

| File | Purpose |
|------|---------|
| `stock_market_dashboard_export.ipynb` | Python notebook — data processing and BI export pipeline |
| `stock_market_dashboard.twbx` | Tableau packaged workbook — full interactive dashboard |
| `stock_historical_for_BI.csv` | BI-ready historical price + indicator data |
| `stock_returns_for_BI.csv` | BI-ready daily returns comparison data |
| `stock_monthly_summary_for_BI.csv` | BI-ready monthly return summary |

---

## How to Run

### Requirements
- pandas
- numpy
- statsmodels
- prophet

### Install
```bash
pip install pandas numpy statsmodels prophet
```

1. Download `cleaned_stock_data.csv` from `Cohort-3 → Stock Market → Data Cleaning`
2. Upload it to Google Colab
3. Run `stock_market_dashboard_export.ipynb` to generate the 3 BI CSV files
4. Open `stock_market_dashboard.twbx` in Tableau Desktop

---

## ✅ Checklist

- [x] Export predictions and historical data for BI
- [x] Build interactive financial dashboard (Tableau)
- [x] Write executive summary on forecast reliability
- [x] Publish GitHub repository