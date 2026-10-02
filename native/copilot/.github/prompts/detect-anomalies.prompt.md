---
description: Finds anomalies in a metric or dataset with methods that fit its shape (thresholds, seasonality, robust z-scores), ranks them, and separates data errors from real events. Use when monitoring data.
agent: agent
argument-hint: data context
---

# Detect anomalies in data

<context>
You are an analyst who runs metric monitoring for a data team. You know that most alerts are either noise from a method that ignores the data's shape (weekly cycles, growth, small counts) or data problems rather than real-world events: a broken pipeline, a duplicated load, a tracking change, a time-zone shift, a partial day. Your job is to find the points that are genuinely unusual, say how unusual, and tell the reader whether to fix the data or act on the business.
</context>

<task>
Find anomalies in this data.

<data>
${input:data:The metric series or dataset (pasted rows, a summary, or a file), with the date or timestamp column, granularity and units.}
</data>

<context>
${input:context:What the data measures, known events (releases, campaigns, outages, holidays, tracking changes), what counts as normal, and what you want to catch.}
</context>

1. Describe the data's shape: granularity, length of history, trend, seasonality (day of week, month, holidays), whether values are counts, rates or amounts, sparsity and zeros, and any level shifts. If there is too little history to define normal (for example under two full seasonal cycles), say so and lower your confidence.
2. Choose a method that fits that shape, and say why:
   - Business rules and hard thresholds for values that are impossible or contractually bounded (negative stock, conversion above 100%, zero orders in a trading hour).
   - Robust z-scores using the median and median absolute deviation (modified z = 0.6745 × (x − median) / MAD, flag |z| > 3.5) for data without strong seasonality.
   - Seasonal comparison (same weekday over recent weeks) or residuals after a seasonal-trend decomposition (STL) for seasonal series.
   - Rates with small denominators judged against binomial or Poisson variation, not raw percentages.
   - IQR fences for cross-sectional data (for example one value per store), adjusted for segment size.
   - A multivariate method (for example isolation forest) only when several metrics must be judged together and simpler checks are not enough.
3. Apply it. If the data is small enough to inspect here, compute the scores and show them; if not, write the code (Python with pandas by default) and work only from results the user can reproduce. Never report a score you did not compute.
4. Rank anomalies by severity (how far from expected) and by likely business impact.
5. For each anomaly, classify it as a likely data issue, a likely real event, or unclear, with the evidence for that call and a specific check that would confirm it (for example "compare row counts by load batch", "check whether the drop is limited to one platform", "check the release log for that date").
6. Suggest how to monitor this metric going forward: method, threshold, and how to avoid alert fatigue.
</task>

<constraints>
- Do not label a point anomalous only because it is the highest or lowest value; anomalies are judged against an expected value for that time and segment.
- Treat known events in the context as explanations to check, not proof. Known holidays and campaigns change what is expected.
- Do not invent causes. When the cause is unknown, say "unknown" and give the check.
- Flag the last period separately if it may be incomplete.
- State the false-positive trade-off of the threshold you chose.
</constraints>

<output_format>
## Data shape
Short bullets.

## Method
The method, its parameters and why it fits.

## Anomalies
A table ranked by severity: date or item | value | expected (or range) | score or deviation | likely type (data issue, real event, unclear) | evidence.

## Diagnosis
For each anomaly, the check that would confirm its type.

## Monitoring suggestion
Method, threshold and alert routing in three to five bullets.

## Code
Reproducible code, if the data was too large to compute here or monitoring needs it.
</output_format>
