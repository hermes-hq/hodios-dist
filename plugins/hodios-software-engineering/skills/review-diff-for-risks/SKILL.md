---
name: review-diff-for-risks
description: Assesses what can go wrong when a change reaches production, such as broken contracts, unsafe migrations, rollout order and rollback, and proposes mitigations. Use before deploying a risky change.
license: CC0-1.0
arguments:
  - diff
  - deployment
argument-hint: <diff> [deployment]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: code-review
  source: https://hermes-ide.com/prompts/review-diff-for-risks
  catalog: 2026.1002.2
---

# Review a diff for shipping risks

## Inputs

- `diff` (required): Unified diff, PR URL or branch name to assess.
- `deployment` (optional): How this change ships, for example "continuous deploy to 40 pods behind a load balancer", "mobile app release" or "npm library".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A change can be correct line by line and still cause an outage. Most bad deploys come from a broken contract, a migration that locks a large table, a deploy order nobody planned, or a failure path nobody watched. This review asks one question: what happens when this change meets production, existing data, older clients and the other services around it? It is not a style review and not a full correctness pass.
</context>

<task>
Assess the risk of shipping $diff. If it is a PR URL or branch name, fetch the diff with the tools you have; if you cannot, ask for the diff once and stop.
Only if deployment was provided: How it ships: $deployment
1. Read the whole diff, then state in one sentence what behaviour changes.
2. Check each risk class below and keep only those the diff actually touches:
   - Contracts: public API, wire or serialization formats, events, CLI flags, config keys, environment variables, database schema. Anything that another component, or an older version of this one, reads or writes.
   - Data: migrations (locks, run time on large tables, reversibility), backfills, destructive writes, defaults applied to existing rows.
   - Rollout order: does the change need a specific deploy order between app and migration, or server and client? What breaks while old and new versions run side by side?
   - Failure paths: new network calls, timeouts, retries, idempotency, concurrency, resource limits, error handling.
   - Security surface: permission checks moved or removed, new untrusted input, secrets. Flag these and recommend a dedicated security review instead of doing one here.
   - Blast radius and reversibility: who is affected if it breaks, whether it sits behind a flag, whether rollback loses data.
   - Observability: will anyone know the new path is failing? Logs, metrics, alerts.
3. For each risk, describe the concrete scenario that triggers it: the input, the data state or the deploy step. Drop any risk you cannot tie to a line in the diff.
4. Propose the cheapest mitigation that closes each risk: a flag, an expand-then-contract migration, a guard, a test, a metric.
</task>

<constraints>
- Every risk cites `path:line` from the diff.
- When a risk depends on something outside the diff (callers, other services, table sizes, traffic), name what must be checked instead of assuming the answer.
- Do not comment on style, naming or formatting.
- If the diff is empty or unreadable, say so and stop. Do not invent a change to review.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Risk level
`low`, `medium` or `high`, then one sentence saying why.
## Risks
A table with the columns # | Risk | Where | Scenario | Likelihood | Impact | Mitigation. Highest risk first, at most 8 rows. Write "None found" when there are none.
## Rollout
Numbered steps to ship safely (deploy order, flags, migration phases) and how to roll back. Two lines are enough for a low-risk change.
## Open questions
Questions for the author about what the diff alone cannot answer, or "None".
</output_format>
