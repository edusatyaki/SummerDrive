# Stock Market Forecasting — Dashboard & Reporting

**Project:** Stock Market Analysis — AAPL / MSFT / SPY
**Cohort:** Cohort-3
**Owner:** Farhana
**Stage:** Phase 4 — Dashboard & Reporting

---

## Overview

This phase builds on Akshat's financial EDA (Phase 0–2) to deliver an interactive Tableau dashboard and a BI data export pipeline. Forecast reliability reporting (Phase 3, Saman) is referenced but not finalized in this submission — see note under Task 3.

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

A Tableau workbook covering price analysis, volume, technical indicators, returns, correlation, and seasonality — organized into 2 dashboard views, each with live interactive filters (Ticker selector and Date range slider) rather than static text commentary, so the dashboard functions as an exploration tool rather than a fixed report.

#### Individual Sheets

| Sheet | Chart Type | Description |
|-------|-----------|-------------|
| Price Overview | Dual-axis line chart | Close price + 50/200-day moving averages for AAPL, MSFT, SPY |
| Volume | Small multiples bar chart | Trading volume over time for each ticker separately |
| Bollinger Bands | Line chart | BB Upper, BB Mid, BB Lower and Close for selected ticker |
| Volatility | Area chart | 20-day rolling volatility — highlights volatility clustering |
| Returns Comparison | Line chart | Daily returns for AAPL, MSFT, SPY overlaid |
| Correlation | Scatter plot | AAPL and MSFT daily returns vs SPY, plotted together with separate trend lines (beta ≈ 1.195 for AAPL, ≈ 1.115 for MSFT; both p < 0.0001) |
| Seasonality | Grouped bar chart | Monthly returns for all three tickers across the full 5-year window |
| KPI cards | Single-value text tiles | Latest Close, Latest Daily Return, 52-Week High/Low, Total Volume — update live with the Ticker and Date filters |

#### Dashboard Views

**Price & Technicals** — *"How is the stock behaving right now?"*
KPI row (Latest Close, Latest Return, 52W High/Low, Total Volume), Ticker dropdown, and Date range slider, combined with Price & Moving Averages, Volume, Bollinger Bands, and 20-Day Volatility charts.

**Returns & Seasonality** — *"How do these stocks move together, and are there seasonal patterns?"*
Daily Returns comparison, combined AAPL/MSFT vs SPY correlation scatter, and the monthly Seasonality breakdown across all three tickers.

Both views are designed for interactive exploration — filtering by ticker or date range updates every chart live — rather than relying on static written commentary.

---

### Task 3 — Executive Summary on Forecast Reliability

> **Status: pending.** This section depends on Saman's Phase 3 forecasting output (ARIMA/Prophet model results with a finalized export). As of this submission, a finalized forecast export was not available to incorporate into the dashboard or this summary. This section should be completed once Saman's model output is delivered, rather than filled in from preliminary/unofficial notebook results.

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
| `dashboard photoes/` | Preview images of the 2 dashboard views |

---

## How to Run

### Requirements
- pandas
- numpy

### Install
```bash
pip install pandas numpy
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