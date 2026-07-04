#  A-B Test / Data Analysis

**Owner:** Akshat Agrawal
**Role:** Statistics & Exploratory Data Analysis (EDA)

## Purpose

This repository contains the data analysis workflow for the A/B Testing project. It focuses on exploring the cleaned dataset, performing statistical analysis, identifying user behavior patterns, and generating business insights to evaluate the effectiveness of the advertising campaign.

## Project Scope

* Import the cleaned dataset
* Perform Exploratory Data Analysis (EDA)
* Analyze conversion rates across test groups
* Conduct statistical hypothesis testing
* Visualize user behavior and conversion trends
* Quantify the business impact of the experiment
* Document findings for the dashboard and final report

## Analysis Included

### Exploratory Data Analysis (EDA)

* Data validation
* Group distribution
* Conversion rate analysis
* Feature exploration

### Statistical Analysis

* Chi-Square Test
* Hypothesis Testing (H₀ vs H₁)
* P-value interpretation
* Cohen's *h* (Effect Size)
* 95% Confidence Intervals
* Group Imbalance Analysis
* Statistical Power Analysis

### Visualizations

* Dose-Response Curve
* Hourly Conversion Analysis
* Peak & Trough Detection
* Day × Hour Heatmap

### Business Impact

* Incremental Conversion Lift
* Estimated Additional Conversions
* Key Business Insights

## Project Checklist

* [x] Clean dataset imported from the Data Cleaning module
* [x] Exploratory Data Analysis completed
* [x] Statistical tests performed
* [x] Visualizations created
* [x] Business impact calculated
* [x] Insights documented
* [x] Findings shared with Dashboard and Report teams

## Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* SciPy
* Statsmodels
* Jupyter Notebook

## Repository Structure

```text
Cohort-3/
└── A-B Test/
    └── Data Analysis/
        ├── data/
        ├── notebooks/
        ├── images/
        ├── README.md
        └── requirements.txt
```

## Outcome

The analysis evaluates whether the advertisement campaign significantly improves conversion rates compared to the PSA group, identifies user engagement patterns, and measures the campaign's overall business impact through statistical and visual analysis.
