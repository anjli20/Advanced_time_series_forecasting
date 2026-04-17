# Advanced Time Series Forecasting — French Bakery Daily Sales

An end-to-end forecasting pipeline for daily sales data from a French bakery dataset.
The project progresses from simple baseline models through ARIMA and SARIMA, then
incorporates exogenous variables and engineered time features. Models are evaluated
using both holdout validation and rolling cross-validation, with the best model used
to generate 7-day future forecasts with prediction intervals.

## Dataset

- Source: French Bakery Daily Sales Dataset
- URL: https://raw.githubusercontent.com/marcopeix/youtube_tutorials/main/data/daily_sales_french_bakery.csv
- Shape: 56,904 rows x 4 columns
- Products: 121 unique bakery items
- Date range: 2021-01-02 to 2022-09-30
- Columns: unique_id (product), ds (date), y (daily sales), unit_price

Focus products for advanced modelling: BAGUETTE and CROISSANT

## Pipeline Overview

1. Load and clean data — filter short series, handle missing values
2. Exploratory data analysis — series lengths and visualisation
3. Holdout split — last 7 days of each series reserved for testing
4. Baseline model evaluation across all 121 products
5. Advanced model evaluation (ARIMA, SARIMA) on selected products
6. Rolling cross-validation with 8 windows and step size of 7
7. SARIMA with product price as exogenous variable
8. SARIMA with engineered time features — Fourier terms, day, week, month
9. Final model selected by lowest MAE
10. Future 7-day forecasts with 80% and 95% prediction intervals

## Models Compared

| Model | Category |
|---|---|
| Naive | Baseline |
| Historic Average | Baseline |
| Window Average (7-day) | Baseline |
| Seasonal Naive (season=7) | Baseline |
| ARIMA (AutoARIMA, non-seasonal) | Advanced |
| SARIMA (AutoARIMA, season=7) | Advanced |
| SARIMA + Price Exogenous | Advanced + Exogenous |
| SARIMA + Time Features (Fourier + day/week/month) | Advanced + Feature Engineering |

## Evaluation Metrics

| Metric | Description |
|---|---|
| MAE | Mean Absolute Error |
| RMSE | Root Mean Squared Error |
| SMAPE | Symmetric Mean Absolute Percentage Error |
| MAPE | Mean Absolute Percentage Error |
| MASE | Mean Absolute Scaled Error (scaled by seasonal naive) |
| Scaled CRPS | Probabilistic forecast accuracy (interval quality) |

## Tech Stack

| Library | Purpose |
|---|---|
| statsforecast | AutoARIMA, SeasonalNaive, StatsForecast framework |
| utilsforecast | Evaluation, plotting, feature engineering |
| pandas / numpy | Data loading and manipulation |
| matplotlib | Metric bar charts and forecast plots |
