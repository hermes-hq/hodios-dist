<context>
Indexes drift away from the workload. Queries change, new access paths go unindexed, old indexes stay on every write long after the query that needed them was deleted, two people add the same index under different names, and heavily updated indexes bloat. Each index speeds up some reads and slows every insert, every update to its columns and every delete, uses disk and memory, and (in PostgreSQL) can stop updates from being heap-only. A useful review weighs both sides with the real workload, not rules of thumb.
</context>

<task>
Review the indexes of this PostgreSQL database.

Schema and indexes:
[SCHEMA_AND_INDEXES]

Workload and statistics:
[SLOW_QUERIES_OR_STATS]

1. Map each top query to its access path: the filter, join, sort and grouping columns, and the index it uses or should use. Note selectivity where the statistics allow.
2. Missing indexes: for queries that scan large tables or sort without an index, propose an index with the column order justified (equality columns first, then range, then sort), and consider a partial index for a selective constant filter, a covering index (`INCLUDE` in PostgreSQL, extra trailing columns in MySQL) for hot read paths, and an expression index when the query wraps the column in a function. Check foreign-key columns used in joins or cascading deletes.
3. Unused indexes: those with no or very few scans since the last statistics reset. Before proposing a drop, rule out indexes that back primary keys, unique constraints or foreign keys; indexes used only on replicas (statistics are per server); and indexes needed by rare but important jobs (month-end reports). Say how long the statistics cover.
4. Duplicate and redundant indexes: identical definitions, and indexes that are a left prefix of another index with the same properties. Keep the one that serves a constraint or the most queries.
5. Bloat and low value: indexes much larger than their data suggests, low-selectivity indexes the planner rarely uses (booleans, status columns without a partial predicate), and wide indexes on heavily updated columns.
6. For every proposed change, estimate the write cost (indexes touched per insert and update on that table, effect on heap-only updates in PostgreSQL), the storage change, and the read benefit tied to specific queries.
7. Write the DDL in a safe order: create new indexes concurrently or online first, verify that plans use them, then drop the indexes they replace. For drops, prefer a reversible step where the engine has one (`ALTER TABLE ... ALTER INDEX ... INVISIBLE` in MySQL 8.0) and keep the `CREATE` statement to restore each dropped index.

If the workload data does not cover enough time to call an index unused, say so and mark those findings as provisional.
</task>

<constraints>
- Tie every recommendation to a query or a statistic in the input. Do not propose indexes for queries you were not shown.
- Use the named engine's syntax and behaviour; say when a feature needs a minimum version.
- Never drop an index that enforces a constraint. Never propose a drop without its restore statement.
- Prefer fewer, well-chosen indexes. If a new index makes an existing one redundant, say so in the same finding.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Summary
Three to five lines: the biggest wins, the safe drops, and the overall write-cost change.

## Findings
Table: # | type (missing, unused, duplicate, bloated, low value) | table and index | evidence (query or statistic) | action | read benefit | write and storage cost | confidence.

## DDL plan
Ordered SQL in code blocks: creates first, verification, then drops with their restore statements commented next to them.

## Verification
The `EXPLAIN` or `EXPLAIN ANALYZE` to run before and after for each affected top query, and the statistics to watch for a week after the change.

## Missing data
What would raise confidence (longer statistics window, replica statistics, bloat estimates) and the queries to collect it.
</output_format>
