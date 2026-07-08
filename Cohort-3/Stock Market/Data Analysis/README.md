# Stock Market EDA and Forecasting — Project README

## Overview

This project performs exploratory data analysis, technical analysis, statistical testing,
and time series forecasting on a daily stock price dataset covering three tickers: AAPL,
MSFT, and SPY. The work is organized into two notebooks, each addressing a distinct set of
objectives, as summarized below.

## Dataset

**File:** `cleaned_stock_data.csv`

The dataset contains daily Open, High, Low, Close, and Volume (OHLCV) values for AAPL, MSFT,
and SPY, spanning June 30, 2021 to June 29, 2026 (1,254 trading days). The file was supplied
in a wide, multi-header format consistent with a standard multi-ticker export, and was
reshaped into a separate clean table per ticker before analysis. No missing values were
present in the dataset. AAPL was used as the primary ticker throughout unless otherwise
noted; the code is parameterized so that the same analysis can be re-run for MSFT or SPY.

## Deliverables

1. **`stock_eda_forecasting_executed.ipynb`** — Financial EDA, technical indicators, and
   forecasting models (Phase 2 and Phase 3).
2. **`advanced_statistical_eda_executed.ipynb`** — Supplementary statistical analysis,
   including hypothesis testing, regression, and unsupervised learning methods.

Both notebooks were executed in full and contain the corresponding output (tables and
charts) alongside the code that produced them.

---

## Notebook 1: Financial EDA and Forecasting

### Phase 2 — Financial EDA and Technicals

**1. Interactive Candlestick Chart**
An interactive candlestick chart was built using Plotly, displaying daily Open, High, Low,
and Close values with a range slider for zooming into specific periods.

**2. SMA and EMA (50-day and 200-day) with Crossover Detection**
Simple Moving Averages (SMA) and Exponential Moving Averages (EMA) were calculated over
50-day and 200-day windows. Crossover points between the two SMAs were programmatically
identified: a Golden Cross (SMA50 crossing above SMA200, typically read as a bullish signal)
and a Death Cross (SMA50 crossing below SMA200, typically read as a bearish signal). Across
the full period, the AAPL series produced five Golden Crosses and four Death Crosses.

**3. Bollinger Bands and Volatility Clustering**
Bollinger Bands were constructed using a 20-day moving average and two standard deviations.
The normalized band width was plotted as a direct visual measure of volatility over time.
Volatility clustering was additionally confirmed statistically by computing the
autocorrelation of absolute daily returns, which remained positive across the first ten
lags (approximately 0.20 at lag 1), indicating that large price movements tend to be
followed by further large movements.

**4. Monthly and Day-of-Week Seasonality**
Average daily returns were grouped by calendar month and by weekday and visualized as bar
charts. Given that the dataset spans five years, each calendar month is represented by only
approximately five independent observations; any apparent seasonal pattern should therefore
be treated as descriptive rather than statistically conclusive without a formal significance
test.

### Phase 3 — Forecasting Models

**1. Augmented Dickey-Fuller (ADF) Test**
The ADF test was applied to the raw closing price series and to the first difference of the
log price (log returns). The price level was found to be non-stationary (p-value
approximately 0.78), while the log returns were found to be stationary (p-value
approximately 0.000). This result established a differencing order of d = 1 for the
subsequent ARIMA-family model.

**2. Chronological Train/Test Split**
The dataset was split by date, with the final 30 trading days withheld as a test set and all
preceding observations used for training. No shuffling was applied, preserving temporal
order as required for time series validation.

**3. SARIMA Model and 30-Day Forecast**
A grid search over (p, q) combinations, with d fixed at 1 based on the ADF test result, was
conducted using Akaike Information Criterion (AIC) as the selection metric. The selected
model was ARIMA(0,1,2). This model was used to generate a 30-day forecast with an associated
95 percent confidence interval, plotted against the actual held-out prices.

**4. Facebook Prophet Model with Holidays**
A Prophet model was fitted with weekly and yearly seasonality components enabled, and United
States holidays incorporated via the built-in country holidays feature. The forecast horizon
was generated on a business-day frequency to align with the equity market trading calendar.

**5. Model Evaluation**
Both models were evaluated on the 30-day test set using Root Mean Squared Error (RMSE) and
Mean Absolute Percentage Error (MAPE). The SARIMA model produced an RMSE of approximately
9.7 and a MAPE of approximately 2.6 percent. The Prophet model produced an RMSE of
approximately 23.1 and a MAPE of approximately 6.9 percent. The SARIMA model outperformed
Prophet on this particular test window, which included a sharp short-term price movement in
the underlying series.

---

## Notebook 2: Advanced Statistical EDA

This notebook extends the analysis with additional statistical methods and does not repeat
any chart or model already covered in Notebook 1.

### Descriptive Statistics and Distribution Analysis

Summary statistics (mean, standard deviation, quartiles, skewness, and kurtosis) were
computed for price and return series. AAPL daily returns exhibited an excess kurtosis of
approximately 6.8, indicating substantially fatter tails than a normal distribution.

**Normality Testing:** The Jarque-Bera and Shapiro-Wilk tests were applied to daily returns.
Both tests rejected the null hypothesis of normality at conventional significance levels,
consistent with the fat-tailed behavior commonly observed in financial return series. This
was supported visually with a histogram overlaid against a fitted normal distribution and a
quantile-quantile (Q-Q) plot.

**Central Limit Theorem Demonstration:** Repeated random sampling of daily returns at
increasing sample sizes (n = 2, 5, 30, 100) was used to construct empirical sampling
distributions of the mean. The skewness of these sampling distributions decreased from
approximately 0.31 at n = 2 to approximately 0.05 at n = 100, illustrating convergence
toward normality as sample size increases, despite the non-normality of the underlying
individual returns.

### Hypothesis Testing

**t-tests:** A one-sample t-test was used to assess whether the mean daily return of AAPL
differed significantly from zero. An independent two-sample t-test was used to compare mean
daily returns between AAPL and SPY. Neither test produced a statistically significant result
at the 0.05 level.

**ANOVA:** One-way ANOVA was applied to compare mean daily returns across the three tickers,
and separately across the five weekdays for AAPL. Neither comparison produced a
statistically significant result.

**Chi-Square Test of Independence:** Daily returns were categorized as "up day" or "down
day" and cross-tabulated against day of the week. A chi-square test of independence was
applied to this contingency table. The result did not indicate a statistically significant
association between weekday and return direction.

**Non-Parametric Tests:** Given the confirmed non-normality of returns, the Mann-Whitney U
test (a non-parametric alternative to the two-sample t-test) and the Kruskal-Wallis test (a
non-parametric alternative to one-way ANOVA) were applied as robustness checks. Both
produced conclusions consistent with their parametric counterparts.

### Correlation, Regression, and Dimensionality Reduction

**Correlation Analysis:** Pearson and Spearman correlation coefficients were computed
between the daily returns of the three tickers. AAPL and SPY returns showed a Pearson
correlation of approximately 0.74; AAPL and MSFT showed a correlation of approximately 0.57.

**Linear Regression (CAPM Market Model):** A single-variable linear regression of AAPL
returns on SPY returns was used to estimate a market beta and alpha, in the style of the
Capital Asset Pricing Model. The estimated beta was approximately 1.20, indicating that AAPL
historically moved somewhat more than the broader market, with an R-squared of
approximately 0.55.

**Regularized Regression (Ridge and Lasso):** A multiple regression model was constructed
using lagged returns of all three tickers together with same-day MSFT and SPY returns as
predictors of AAPL's same-day return. Ordinary least squares, Ridge regression, and Lasso
regression were compared. The Lasso model reduced the coefficients on all three lagged
return features to zero, retaining only the same-day SPY and MSFT terms, illustrating
automatic feature selection under L1 regularization in the presence of weak and collinear
predictors.

**Principal Component Analysis (PCA):** PCA was applied to the standardized returns of the
three tickers. The first principal component explained approximately 78 percent of total
variance, with approximately equal, same-signed loadings across all three tickers,
indicating that a single common market factor accounts for the majority of shared movement
across AAPL, MSFT, and SPY.

### Clustering

**K-Means Clustering:** Trading days for AAPL were clustered into three groups based on
daily return and 20-day rolling volatility, without any predefined labels. The resulting
clusters separated into a small, distinct group of high-volatility, negative-return days
(approximately 89 days), alongside two larger, comparatively calmer regimes with differing
average return levels.

### Moving Average Smoothing

A Weighted Moving Average (WMA) was calculated as a supplementary smoothing method, distinct
from the SMA/EMA crossover analysis in Notebook 1. The WMA assigns greater weight to more
recent observations than a simple moving average, and was used here to produce a smoothed
price series.

---

## Summary of Key Findings

- The AAPL closing price series is non-stationary in level but stationary after first
  differencing of log returns, supporting the use of an ARIMA(0,1,2) specification.
- Volatility clustering is present and statistically confirmed through positive
  autocorrelation of absolute returns.
- Daily returns are not normally distributed, exhibiting fat tails, though the sampling
  distribution of the mean approaches normality as predicted by the Central Limit Theorem.
- No statistically significant differences in mean daily returns were found across tickers,
  weekdays, or return direction versus weekday, based on both parametric and non-parametric
  tests.
- AAPL exhibits a market beta of approximately 1.20 relative to SPY, with a single common
  market factor explaining roughly 78 percent of the shared variance across all three
  tickers.
- On a 30-day chronological holdout, the SARIMA model produced lower forecast error than the
  Prophet model, with RMSE of approximately 9.7 versus 23.1, respectively.

## Notes and Limitations

- Seasonality results (monthly and day-of-week) are based on a limited number of
  observations per category and should be interpreted as descriptive rather than
  confirmatory.
- The Ridge and Lasso regression results using same-day predictors reflect contemporaneous
  co-movement between tickers rather than genuine forward-looking predictive power.
- Forecast accuracy for both SARIMA and Prophet is influenced by the presence of a sharp
  short-term price movement within the test window and should not be generalized beyond the
  specific evaluation period used.
