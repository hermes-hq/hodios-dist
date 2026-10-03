---
name: estimate-with-ranges
description: Breaks engineering work into tasks and produces a range estimate with a confidence level, stated assumptions and the unknowns that need a spike. Use when asked "how long will this take?".
license: CC0-1.0
arguments:
  - work
  - team_context
  - unit
argument-hint: <work> [team_context] [unit]
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: prompt
  category: planning
  source: https://hermes-ide.com/prompts/estimate-with-ranges
  catalog: 2026.1003.1
---

# Estimate work as a range

## Inputs

- `work` (required): The work to estimate, a spec, ticket or description, plus what "done" includes (tests, review, rollout, docs).
- `team_context` (optional): Who does the work and their familiarity with the code, availability (meetings, on-call, other projects), and how long similar work took before.
- `unit` (optional; one of: hours, days, points; default: days): Unit for the effort figures.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Single-number estimates are heard as promises and are almost always optimistic: they leave out review, testing, rollout and interruptions, and they hide the parts nobody understands yet. A useful estimate is a range with a stated confidence, built bottom-up from tasks small enough to reason about, and explicit about the assumptions and unknowns that drive the spread. The unknowns that matter most are better resolved with a short, time-boxed spike than argued about.
</context>

<task>
Estimate this work:
$work
Only if team_context was provided: Team context: $team_context
Unit: $unit.
If you do not know who will do the work, how familiar they are with the code, or their real availability, ask once; if the user wants an answer anyway, use the assumptions "one engineer familiar with the codebase, about 60% of their time on this work" and say so.

1. Clarify scope: list what is in and out, including the parts people forget (tests, code review rounds, migrations, feature flags, monitoring, docs, deployment, coordination with other teams). Ask about anything that changes the size by more than about 20%.
   If the work is too vague for a meaningful range, say so, give the questions that would make it estimable, and give a rough order of magnitude only.
2. Break the work into tasks of no more than about two ideal days each. For each task give optimistic, most-likely and pessimistic effort in $unit (ideal engineer-days when the unit is days), and mark its uncertainty (low, medium, high) with the reason. For points, estimate relative to a reference task from the context; if there is none, say that points cannot be calibrated and give days as well.
3. For each high-uncertainty task, define a spike: the question it answers, a time box (normally half a day to two days), and how its answer changes the estimate.
4. Roll up: compute the expected value and spread per task with the three-point (PERT) formula, mean = (O + 4M + P) / 6 and standard deviation = (P − O) / 6, sum the means, and combine spreads (root-sum-square if tasks are independent; note when they are correlated, which widens the range). Under a normal approximation the 50% figure is the summed mean and the 85% figure is the mean plus about one combined standard deviation (z ≈ 1.04). Show the arithmetic.
5. Convert effort to calendar time using availability and parallelism, and add waiting time that is not effort (review latency, other teams, release windows).
6. List the assumptions the estimate depends on, and what would move it most.
</task>

<constraints>
- Never give a single number without its range and confidence.
- Do not pad silently. Every buffer appears as a named line with its reason.
- Do not use velocity, story points or historical figures that were not given; if they would help, ask for them.
- Label every assumption as such.
- An estimate is not a commitment; do not phrase it as one.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Estimate
One sentence: "50% likely within X weeks of starting, 85% likely within Y weeks, assuming Z", then the effort range in ideal days.
## Breakdown
Table: Task | O | M | P | Mean | Uncertainty and reason. Totals row, then the roll-up arithmetic.
## Unknowns and spikes
Table: Unknown | Spike question | Time box | Effect on the estimate.
## Assumptions
Bullets.
## What would change it
The three factors that would move the estimate most, and in which direction.
## Not included
Bullets: work outside this estimate.
</output_format>
