---
name: plan-zero-downtime-schema-change
description: Turns the current table DDL and a desired change into expand and contract steps, each with lock-safe SQL, the app change, backfill, verification and rollback. Use before altering a live table.
license: CC0-1.0
arguments:
  - current_schema
  - desired_change
  - engine
argument-hint: <current_schema> <desired_change> [engine]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data
  source: https://hermes-ide.com/prompts/plan-zero-downtime-schema-change
  catalog: 2026.1002.0
---

# Plan a zero-downtime schema change from DDL

## Inputs

- `current_schema` (required): The exact CREATE TABLE statements for the affected tables, including indexes, constraints, triggers and foreign keys, plus row counts and write rates if known.
- `desired_change` (required): The target state, for example "split users.name into first_name and last_name" or "change orders.amount from float to numeric(12,2)".
- `engine` (optional; one of: postgres, mysql, sqlite, sql-server, other; default: postgres): Database engine. Mention the major version in desired_change if you know it.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
The exact DDL decides what is safe. The same `ALTER TABLE` can be instant on one table and a table rewrite on another, depending on the column type, default, constraints, indexes, triggers and engine version. Even an instant change can stall production: it queues behind a long-running transaction while holding a lock request that blocks every query after it. And during any deploy, old and new application versions run side by side, so each intermediate schema must work with both. The safe shape is expand, migrate, contract: add the new structure, write to both, backfill, switch reads, stop writing the old, then remove it, with every step independently deployable and reversible.
</context>

<task>
Current schema ($engine):
$current_schema

Desired change: $desired_change

1. Read the DDL and list what affects safety: table size and write rate if given, column types, defaults, NOT NULL and CHECK constraints, unique indexes, foreign keys in both directions, triggers, generated columns, and replication. Say what is missing and what you assume about it.
2. Break the change into ordered steps. For each step give:
   - the SQL, using the engine's lock-safe forms (see the notes below), with a lock timeout and a retry instruction for any statement that takes a strong lock;
   - the lock it takes, whether it rewrites or scans the table, and the expected duration class (instant, proportional to table size, or batched);
   - the application change that ships with it (write both, read new behind a flag, stop writing old);
   - the verification query that must pass before the next step;
   - the rollback for that step.
3. For backfills: batch by primary key range, keep each batch in a short transaction, make it idempotent so it can resume, throttle by replication lag or load, and give the query that proves completeness.
4. For dual writes, choose application-level writes or a temporary trigger, say why, and say how drift between old and new columns is detected and repaired.
5. Mark the point of no return: the first step after which rolling back means restoring data, not just redeploying.

Engine notes. Check each against the stated version:
- postgres: use `CREATE INDEX CONCURRENTLY` (outside a transaction; drop the invalid index if it fails), add constraints `NOT VALID` and then `VALIDATE CONSTRAINT`, enforce NOT NULL through a validated `CHECK (col IS NOT NULL)` before `SET NOT NULL`, and know that most type changes rewrite the table. Set `lock_timeout` on every DDL session.
- mysql: say which `ALGORITHM` (INSTANT, INPLACE or COPY) and `LOCK=NONE` apply, watch metadata locks, and use an online schema change tool (gh-ost or pt-online-schema-change) when the operation would copy the table.
- sqlite: most changes need the documented create-copy-rename table rebuild. There is one writer at a time, so plan for a short write pause rather than true zero downtime, and say so.
- sql-server: say which operations are metadata-only and which need `ONLINE = ON`, and note that online index operations depend on the edition.
- other: ask which engine and version before giving SQL.
</task>

<constraints>
- Never combine the expand and contract phases in one deploy.
- Every step must leave the currently deployed application version working.
- Do not claim an operation is instant or online unless that is true for the engine and version. If it depends on the version, say so.
- Do not drop or rename anything still read by any deployed code. Say how to confirm that nothing reads it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Summary
Two or three sentences: the approach, the number of deploys, and the riskiest step.

## Compatibility matrix
Table: step | schema state | app version that must work | reads from | writes to.

## Steps
Numbered. Each: SQL in a fenced block, lock and duration, app change, verification query, rollback.

## Point of no return
The step, and what rollback means after it.

## Risks
Bullets: the risk, how to detect it, and the mitigation.
</output_format>
