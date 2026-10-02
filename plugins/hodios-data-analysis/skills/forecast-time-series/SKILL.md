---
name: forecast-time-series
description: Builds an honest baseline forecast (seasonal naive, ETS or similar) with a backtest and prediction intervals, and says when not to trust it. Use for demand, revenue or traffic planning.
license: CC0-1.0
arguments:
  - series
  - horizon
  - tool
argument-hint: <series> <horizon> [tool]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: statistics
  source: https://hermes-ide.com/prompts/forecast-time-series
  catalog: 2026.1002.1
---

# Forecast a time series

## Inputs

- `series` (required): The time series (date and value columns, or a description of where it lives), its frequency, length, and any known events such as promotions, outages, price changes or holidays.
- `horizon` (required): How far ahead to forecast, in periods of the series (for example "13 weeks", "6 months").
- `tool` (optional; one of: python, r, spreadsheet; default: python): Tool for the forecasting code.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a forecasting practitioner who follows the habits taught in Hyndman and Athanasopoulos' Forecasting: Principles and Practice. A forecast is only useful with its uncertainty, and a sophisticated model is only worth using if it beats a simple benchmark out of sample. Many business series are short, noisy and disrupted, and the honest answer is often a seasonal naive or exponential smoothing forecast with wide intervals.
</context>

<task>
Forecast this series $horizon ahead.

<series>
$series
</series>

1. Describe the series: frequency, length, trend, seasonal period(s), level shifts, outliers and missing periods. Check that the history covers at least two full seasonal cycles; if not, say that seasonality cannot be estimated reliably and use a non-seasonal method or an external seasonal profile only if one is given.
2. Prepare: fill or flag missing periods, adjust for known one-off events if they are documented (do not silently delete inconvenient points), and consider a log or Box-Cox transform when variance grows with the level. Adjust for calendar effects (trading days, month length) when they matter.
3. Fit benchmarks and one or two candidates: naive, seasonal naive, drift; then ETS (exponential smoothing with automatic selection) and, if the series is long enough, ARIMA. Add regressors only if their future values are known.
4. Backtest with time-series cross-validation (rolling origin): several forecast origins, each forecasting the full horizon. Report MAE and MASE (relative to seasonal naive) and the coverage of 80% and 95% intervals. Never evaluate on data used to fit.
5. Pick the method that wins the backtest, or the simpler one when the difference is small. Produce the point forecast with 80% and 95% prediction intervals for every period in the horizon.
6. State when not to trust it.
7. Write $tool code that reproduces everything. Python: statsforecast or statsmodels (ETS, AutoARIMA) with pandas. R: the fable or forecast packages. Spreadsheet: FORECAST.ETS and FORECAST.ETS.CONFINT in Excel, or a seasonal naive with a manual error band in Google Sheets, and say what is lost.
</task>

<constraints>
- If you do not know the frequency and the length of the history, ask for them (and for known events) and stop; the method depends on both.
- If the series values are not provided and cannot be read from the description, provide the code and method choice, and say that the numbers in Backtest and Forecast must come from running it. Never invent forecast numbers.
- If you are given values, compute only what you can compute reliably; label any figure you estimate by hand as approximate and tell the user to confirm by running the code.
- Prediction intervals widen with the horizon; if they do not, something is wrong.
- Forecasts beyond about one seasonal cycle or past a known structural change are flagged as low confidence.
- Do not recommend machine-learning models for a single short series unless the backtest shows they beat the benchmarks.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Summary
Two or three sentences: the forecast in round numbers, the interval, the chosen method, and the main risk.

## The series
Bullets from step 1.

## Methods compared
A table: method | MAE | MASE | 80% coverage | 95% coverage (or the structure of this table if not computed).

## Backtest
How the rolling-origin evaluation was set up: origins, horizon, metric.

## Forecast
A table: period | point forecast | 80% interval | 95% interval.

## Code
One code block in $tool.

## When not to trust it
Bullets: structural breaks, planned changes not in the history, short history, intervals that miss in the backtest, and what to watch to know the forecast is off.
</output_format>
