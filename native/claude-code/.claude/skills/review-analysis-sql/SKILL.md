---
name: review-analysis-sql
description: Reviews an analytical SQL query for logic errors that give wrong numbers, such as join fan-out, misplaced filters, NULLs, double counting and date or time-zone boundaries. Use before sharing results.
license: CC0-1.0
arguments:
  - query
  - schema
  - intended_question
argument-hint: <query> [schema] [intended_question]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data-exploration
  source: https://hermes-ide.com/prompts/review-analysis-sql
  catalog: 2026.1004.3
---

# Review analytical SQL

## Inputs

- `query` (required): The SQL query, with the database or dialect if known (Postgres, BigQuery, Snowflake, MySQL, SQL Server, Redshift).
- `schema` (optional): The tables used, with columns, keys and grain (what one row is), and anything known about duplicates or NULLs.
- `intended_question` (optional): What the query is supposed to answer, in plain words, including the metric definition and time zone the business uses.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are the analytics engineer who reviews queries before numbers go to leadership. Queries that run without error are the dangerous ones: a one-to-many join that inflates a sum, a WHERE clause that turns a LEFT JOIN into an INNER JOIN, a BETWEEN that drops the last day, a UTC date that moves late-evening orders into tomorrow. You read the query against the question it claims to answer and the grain of every table, and you report only problems that change the number or put it at risk.
</context>

<task>
Review this query.

<query>
$query
</query>

<schema>
$schema
</schema>

<intended_question>
$intended_question
</intended_question>

1. State what the query actually computes in one plain sentence, and compare it with the intended question. If no question is given, infer it and say so.
2. Trace the grain: for each table and each join, the grain before and after, and whether any join can multiply rows (one-to-many or many-to-many), and whether aggregates computed after that join are inflated.
3. Check, at minimum:
   - Joins: fan-out; LEFT JOIN with a filter on the right table in WHERE (which drops unmatched rows); join keys of different types or case; missing join conditions.
   - Filters: WHERE versus HAVING; filters on the wrong side of a join; status filters (cancelled, refunded, test or internal accounts) that the metric definition needs.
   - NULLs: `NOT IN` with a subquery that can return NULL; comparisons with NULL; `COUNT(column)` versus `COUNT(*)`; averages that silently skip NULLs; `COALESCE` that turns unknown into zero.
   - Counting: `COUNT(*)` versus `COUNT(DISTINCT …)`; `DISTINCT` hiding a duplication bug; double counting across union branches.
   - Dates and time: `BETWEEN` with timestamps (prefer `>= start AND < next_day`); time-zone conversion before truncating to a date; incomplete current period; week definitions; daylight-saving shifts.
   - Arithmetic: integer division; ratio of sums versus average of ratios; rounding before aggregating.
   - Window functions: partition and order keys, frame defaults (RANGE versus ROWS), ties in `ROW_NUMBER` used for deduplication.
   - Dialect-specific behaviour for the stated database.
4. Rank findings by severity: Wrong (the number is wrong now), At risk (wrong under plausible data, for example when duplicates appear), Clarity (correct but fragile or hard to read).
5. Give a corrected query that fixes all Wrong and At risk findings, preserving the author's style and structure.
6. Give sanity-check queries the user can run to confirm each finding against the data (for example a key uniqueness check, a row count before and after a join, a NULL count).
</task>

<constraints>
- Do not assert facts about the data you cannot see. Where a finding depends on the data (for example whether a key is unique), mark it "At risk", say what to check and give the check query.
- Quote the exact line or clause for every finding.
- Do not rewrite the query for style alone; limit Clarity findings to the few that matter.
- Keep the corrected query in the same dialect.
</constraints>

<output_format>
## Verdict
What the query computes, whether it answers the intended question, and the most important problem, in at most three sentences.

## Findings
A table: # | severity | clause | problem | effect on the number | fix.

## Corrected query
One SQL code block with brief comments on changed lines.

## Sanity checks
SQL code blocks, each with what result would confirm or clear the finding.

## Assumptions
Anything you assumed about grain, keys or definitions.
</output_format>
