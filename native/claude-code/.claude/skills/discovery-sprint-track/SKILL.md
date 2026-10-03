---
name: discovery-sprint-track
description: Runs a two-week discovery sprint from problem framing and assumption mapping through interviews, synthesis and tests to a decision readout, pausing for the team between steps.
license: CC0-1.0
arguments:
  - opportunity
  - target_users
  - constraints
argument-hint: <opportunity> <target_users> [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: product-discovery
  source: https://hermes-ide.com/prompts/discovery-sprint-track
  catalog: 2026.1003.1
---

# Discovery sprint track

## Inputs

- `opportunity` (required): The opportunity or problem area to explore, why it matters now, and any evidence or hunches that triggered it.
- `target_users` (required): Who the sprint is about (segment, role, situation) and how the team can reach them (customer list, panel, community, sales contacts).
- `constraints` (optional): Team members and their availability, budget for incentives or tools, fixed dates, and anything off-limits. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs a two-week discovery sprint for a product trio (product manager, designer, engineer) on this opportunity:

<opportunity>
$opportunity
</opportunity>

Target users:

<target_users>
$target_users
</target_users>
Only if constraints was provided: 

Constraints:

<constraints>
$constraints
</constraints>

Six steps: frame the problem and decision, map the assumptions, plan interviews, synthesise them, design cheap tests, and write the decision readout. Typical calendar: days 1-2 framing and assumptions, days 2-8 recruiting and interviews, day 9 synthesis, days 9-13 tests, day 14 readout; adjust to the constraints.

Each step produces one document and stops for the team's edits or approval; later steps build on approved versions. Steps that need real-world work wait for the team to paste notes or results. Never invent findings, quotes, numbers or results: missing facts become questions or marked placeholders. The team owns every decision.

## Steps

Work through these steps in order. Do not skip a gate.

1. frame (discover)
2. assumptions (plan)
3. interviews (plan)
4. synthesis (discover)
5. tests (design)
6. readout (review)

### Step 1: Frame the problem and the decision

1. If the business outcome at stake, the readout date or who decides afterwards is missing, ask for those in one message and stop. Other gaps (what is already known, the trio's hours) do not block the framing: mark them as placeholders in the plan.
2. Write:
   - **Problem statement:** who has the problem, when, what they do today and why it matters. No solution words.
   - **Decision to inform:** for example invest, narrow or drop, and who makes it.
   - **Sprint questions:** three to five, each answerable with evidence.
   - **Out of scope.**
   - **Success signals:** what would justify investing, set now, before any data.
   - **Plan:** a day-by-day calendar with owners, including recruiting lead time.
3. Flag any question the team cannot answer in two weeks with its access, and propose a narrower one.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 2 (assumptions).

### Step 2: Map and rank the assumptions

1. List the assumptions the opportunity depends on as testable statements, across desirability (the problem is real, frequent, painful; users would switch), usability, feasibility, viability (pricing, cost to serve, channel, compliance) and ethics.
2. Rate each on importance (does the opportunity collapse if it is false?) and evidence (real evidence, not opinion). Sort into: test first (important, little evidence), proceed, watch, ignore.
3. Shortlist the two or three riskiest. For each, say whether interviews can test it (past behaviour, frequency, workarounds, spend) or it needs a behavioural test later (willingness to pay, adoption, usability).
4. Point out sprint questions with no assumption behind them, and risky assumptions no question covers.

Output a table (assumption | type | importance | evidence | quadrant | how to test) and the shortlist. Stop for approval.

**Gate:** stop here and wait for the user's approval before step 3 (interviews).

### Step 3: Plan and recruit interviews

1. **Who:** segments to cover, five to eight interviews per main segment (say what fewer costs in confidence), plus one or two people without the problem as contrast.
2. **Screener:** four to six questions on recent behaviour ("In the last month, how often…?"), not revealing the qualifying answer, with disqualifiers and incentive.
3. **Invitation:** short and honest, for the team's channel: time needed, purpose (learning, not selling), data use.
4. **Guide** for 30-45 minutes: warm-up; the story of the last specific time the problem happened, with probes for trigger, actions, people, cost and past attempts; probes labelled by the assumption they inform. No pitching, no "would you use" or "how much would you pay". Show a concept, if at all, only at the end.
5. **Notes template:** context, story, verbatim quotes, evidence for or against each assumption, surprises.
6. **Logistics:** consent and recording wording, roles, a debrief right after each call.

Stop for approval. After the interviews, the team pastes its notes to start step 4.

**Gate:** stop here and wait for the user's approval before step 4 (synthesis).

### Step 4: Synthesise the interviews

Use only the notes or transcripts provided. If none are pasted, ask for them and stop.

1. Summarise each interview in three lines: who, their story, the strongest evidence.
2. Cluster into themes (needs, pains, workarounds, triggers). For each: participants showing it out of the total, two verbatim quotes with participant labels, and whether it is behaviour or opinion.
3. Update the assumption table: supported, contradicted, mixed or untested, citing participants. Say when the sample is too small to conclude.
4. List surprises and new opportunities, and the sample's limits (who was missing, leading moments).
5. Recommend which assumptions still need a behavioural test and which are settled.

Never add a quote or count not in the notes. Stop for approval.

**Gate:** stop here and wait for the user's approval before step 5 (tests).

### Step 5: Design cheap tests

1. For each open assumption (at most three), pick the cheapest test that yields behaviour within the time left: prototype test, fake door with an honest message, landing page, concierge or Wizard of Oz trial, pre-order or letter of intent, or a data pull. Say what it cannot tell you.
2. Write an experiment card: We believe [assumption]. We will [test] with [audience, sample]. We measure [metric]. Right if [threshold], wrong if [threshold], inconclusive between. Cost, duration, owner. Justify the thresholds now.
3. Ethics: fake doors explain what is real at the click, no one pays for something that does not exist without an immediate refund, data is handled as promised.
4. Give a schedule that ends before the readout.

Stop for approval. The team pastes results to start step 6.

**Gate:** stop here and wait for the user's approval before step 6 (readout).

### Step 6: Decision readout

Write a one-page readout for the decision-maker from the approved synthesis and the test results provided. If results are missing, ask; never assume an outcome.

1. **Recommendation:** invest, narrow, pivot or stop, with confidence (high, medium, low) and why.
2. **What we learned:** each sprint question answered with its evidence, against the success signals and thresholds set earlier. Say plainly when a threshold was missed.
3. **Assumption scorecard:** supported, contradicted, mixed or untested.
4. **Still unknown:** each gap and its cheapest next test.
5. **If we invest:** the problem to solve first, the outcome metric, the first steps. **If we stop:** what is worth keeping.
6. **Appendix:** methods, sample, dates, placeholders for links to raw notes.

The decision belongs to the decision-maker.
