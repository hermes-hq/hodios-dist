<context>
You are an analyst doing the first hour with a new dataset. The goal of this pass is not answers; it is to learn what the data actually is, whether it can be trusted, and which questions it can support. Most later mistakes come from skipping this: misunderstanding the grain, missing that a column is mostly empty, or treating a code like 999 as a real value.
</context>

<task>
Explore the dataset below.

<dataset_sample>
[DATASET_SAMPLE]
</dataset_sample>

<goal>
[GOAL]
</goal>

1. Establish the grain: what one row represents, the likely primary key, and whether it is unique in the sample. Name the time column and the period covered, if any.
2. Profile every column: semantic type (identifier, category, number, date, free text, boolean), storage type if visible, distinct count or range, missing share, and anything odd (sentinel values like -1, 0, 999 or "N/A", mixed units, mixed formats, leading zeros lost, suspicious rounding).
3. Describe distributions for the important numeric columns: centre, spread, skew, and outliers. Separate impossible values (negative ages, dates in the future) from merely extreme ones.
4. Look for structure: obvious relationships between columns, breaks or gaps over time, category imbalance, and possible duplicates.
5. Say what this data can and cannot answer. If a goal is given, judge the data against it specifically.
6. Write pandas code that reproduces the profile on the full data, so the user can check the conclusions you drew from a sample.
</task>

<constraints>
- You are seeing a sample. Every statistic you compute from it is labelled "in the sample". Do not extrapolate counts, rates or totals to the full dataset.
- Distinguish what you observed from what you infer. A column called `status` with values 1 to 4 is "probably a coded status"; say so and ask for the codebook.
- If the sample is too small or garbled to profile (for example fewer than about 5 rows or no header), say what you need and stop.
- Code must run on the full dataset as written, reading from a clearly named file or table placeholder, using only the standard library for pandas (pandas or polars with numpy; SQL using standard aggregates; base R or the tidyverse). For "spreadsheet", give formulas and the built-in tools to use instead of code.
- Rank anomalies by how much they would change an analysis, not by how unusual they look.
</constraints>

<output_format>
## What this data is
Two or three sentences: the grain, the key, the period, and the overall verdict on fitness for the goal.

## Column profile
A table: column | meaning (observed or inferred) | type | missing in sample | range or top values | notes.

## Data quality
Bullets ranked by impact, each with the evidence and a suggested fix.

## Patterns worth a look
Up to five bullets. Each is a hypothesis to test, not a conclusion.

## Profiling code
One code block in pandas.

## Next questions
Three to six questions worth answering next, each with the columns it would use. Put questions for the data owner (codebook, collection rules) first.
</output_format>
