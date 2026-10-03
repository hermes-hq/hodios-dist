---
name: optimize-sql-query
description: Speeds up a slow SQL query from its execution plan, proposing rewrites and indexes with expected gains and their write-cost trade-offs. Use when one query dominates latency or database load.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: performance
  source: https://hermes-ide.com/prompts/optimize-sql-query
  catalog: 2026.1003.0
---

# Optimise a slow SQL query

## Inputs

- [QUERY] (required): The slow query, plus the relevant table definitions, existing indexes and approximate row counts if you have them.
- [PLAN_OUTPUT] (optional): The execution plan with actual timings, e.g. EXPLAIN (ANALYZE, BUFFERS) output or the query profile.
- [ENGINE] (optional; one of: postgres, mysql, sql-server, sqlite, bigquery, snowflake; default: postgres): Database engine the query runs on.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Query tuning without a plan is guessing. The plan shows where time actually goes: which node reads the most rows or buffers, where estimated and actual row counts diverge, where a sort or hash spills to disk. Common advice like "add an index on every WHERE column" adds write cost and often does nothing because the predicate is not sargable, the planner misestimates, or the query reads most of the table anyway. Warehouse engines have no indexes at all, so their fixes are different.
</context>

<task>
Make this [ENGINE] query faster:
[QUERY]
Only if [PLAN_OUTPUT] was provided: 
Execution plan:
[PLAN_OUTPUT]

1. If there is no plan, give the exact command to capture one for [ENGINE] with actual timings (for example EXPLAIN (ANALYZE, BUFFERS) on Postgres, EXPLAIN ANALYZE on MySQL 8, the actual execution plan on SQL Server, EXPLAIN QUERY PLAN on SQLite, the query profile or execution details on BigQuery and Snowflake). Continue with hypotheses, each labelled "unverified until the plan confirms".
2. If table definitions or existing indexes are missing and the advice depends on them, ask for them in the Verify section rather than assuming.
3. Read the plan: find the most expensive nodes, row-estimate errors greater than about 10x (stale statistics or correlated columns), sequential scans with selective filters, nested loops over large inputs, sorts and hashes spilling to disk, and repeated subplans.
4. Look for query-level causes: non-sargable predicates (functions or casts on indexed columns, leading-wildcard LIKE, OR across different columns), implicit type conversions, SELECT of unneeded columns, OFFSET pagination on deep pages, correlated subqueries, and duplicated work.
5. For BigQuery and Snowflake, focus on bytes scanned, partition pruning, clustering, join order and avoiding repeated scans instead of indexes.
6. Propose changes in order of expected gain. For each index, give the exact DDL, explain the column order (equality columns first, then range, then sort; covering or INCLUDE columns where useful), consider a partial index, and check whether it makes an existing index redundant.
</task>

<constraints>
- Every rewrite must return the same results. Call out any semantic difference explicitly, such as NOT IN versus NOT EXISTS with NULLs, or changed duplicate handling.
- State the write cost of each new index: slower inserts and updates, extra storage, and lock or build impact. For production, use the online or concurrent build option where [ENGINE] has one.
- Expected gains are estimates unless the plan proves them. Say which.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Diagnosis
Where the time goes, citing plan nodes and their actual numbers.
## Changes
Numbered, ranked: the change, expected gain, confidence (high/medium/low).
## Rewritten query
A fenced `sql` block, or "No rewrite needed".
## Index changes
Fenced DDL for indexes to add or drop, or "None".
## Trade-offs
Write cost, storage, and any semantic changes.
## Verify
How to confirm the gain: the plan to re-run, the numbers to compare, and any information still needed.
</output_format>
