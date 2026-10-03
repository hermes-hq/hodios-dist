---
name: fix-n-plus-one-queries
description: Finds N+1 database queries behind an endpoint, page or job by counting real queries, fixes them with eager loading or batching, and adds a query-count test so they do not return.
license: CC0-1.0
arguments:
  - target
  - query_log
argument-hint: <target> [query_log]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: performance
  source: https://hermes-ide.com/prompts/fix-n-plus-one-queries
  catalog: 2026.1003.0
---

# Fix N+1 queries

## Inputs

- `target` (required): The endpoint, page, resolver, job or file where you suspect N+1 queries.
- `query_log` (optional): A query log or APM trace from a slow request, if you have one.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
An N+1 query happens when code loads a list with one query and then runs one more query per item, usually through lazy-loaded relations inside a loop or a serializer. It looks fine with test data and collapses with real data. The fix must be proven by counting queries, not by reading the code.
</context>

<task>
Find and fix N+1 queries in: $target
Only if query_log was provided: 
Start from this log or trace:
$query_log

1. Identify the ORM or data layer and how to observe queries: enable query logging or use the framework's query counter or debug tooling.
2. Run the target with enough data to show the pattern (at least 3 items; create fixtures if needed) and count the queries. Record the count and, if available, the time.
3. Trace each repeated query to the code that triggers it: the loop, template, serializer or resolver and the relation it touches, with `path:line`.
4. Fix it with the idiomatic tool for this stack: eager loading (for example select_related or prefetch_related, includes or preload, with, JOIN FETCH or an entity graph, selectinload or joinedload, include), a batched loader such as DataLoader for GraphQL, or one aggregate query where only counts or sums are needed.
5. Choose between a join and a separate batched query deliberately: joining several collections at once multiplies rows, so prefer separate IN-list queries for collections.
6. Re-run and count again. Then add a test that asserts the query count for the target with several items, so the N+1 cannot come back unnoticed.
</task>

<constraints>
- Load only the relations the code actually uses; do not over-fetch whole object graphs.
- Keep the response shape and ordering identical.
- Do not add caching as the fix for an N+1.
- Report real query counts from runs, not from reading the code.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Result
One line: queries before and after for N items, and time if measured.
## Cause
Each N+1: `path:line` — the loop or serializer — the relation loaded per item.
## Fix
The diff, then one sentence per change on why it removes the extra queries.
## Regression guard
The test added and its result.
## Other N+1 patterns spotted
Bullets with `path:line`, not fixed. Or "None".
</output_format>
