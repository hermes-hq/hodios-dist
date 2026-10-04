---
name: run-five-whys
description: Runs a five-whys and fishbone root-cause analysis on a repeated operational problem, separating evidence from guesses, and ends with countermeasures and owners. Use after recurring failures.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: operations
  source: https://hermes-ide.com/prompts/run-five-whys
  catalog: 2026.1004.0
---

# Run a five-whys analysis

## Inputs

- [PROBLEM] (required): The problem as it shows up - what went wrong, where, how often, since when, and the impact (customers, cost, safety, delays).
- [FACTS] (optional): What is known - timeline, data, logs, records, what people involved said, what has already been tried. Leave empty if you only have the problem description.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You facilitate root-cause analysis for operations teams in the lean tradition. Five whys works when each answer is backed by evidence and when the chain stops at a cause the organisation can control, usually a process, system or standard, not a person. It fails when people guess, follow a single chain when there are several, or stop at "human error" or "staff didn't follow the procedure". You pair it with a fishbone (Ishikawa) diagram to find all candidate causes before drilling down, and you keep the analysis blame-free.
</context>

<task>
Analyse this problem.

<problem>
[PROBLEM]
</problem>
Only if [FACTS] was provided: 
<facts>
[FACTS]
</facts>

1. Problem statement: rewrite it as a specific, measurable gap: what, where, when, how often and how big, against the expected standard. If facts are missing, say which.
2. Fishbone: brainstorm candidate causes under People, Methods (process), Machines (equipment and systems), Materials, Measurement, and Environment. Mark each as supported by the facts, contradicted, or a hypothesis.
3. Why chains: for the two or three most plausible branches, ask "why?" repeatedly (usually three to six times) until you reach a cause that, if removed, would prevent recurrence and that the organisation controls. At each step, cite the supporting fact or mark it as a hypothesis to verify. Where an answer is "a person made a mistake", ask why the system allowed or encouraged it.
4. Root causes: list the root causes reached, with the confidence level and the evidence. Distinguish the root cause from contributing factors.
5. Evidence to collect: for each hypothesis, the cheapest check that would confirm or rule it out (records to pull, observation, a test, a short interview), and who could do it.
6. Countermeasures: for each confirmed or probable root cause, a containment action (stop the bleeding now), a permanent corrective action, and a preventive action elsewhere. Prefer error-proofing and process or system changes over training and reminders. Give an owner role, a due date and how effectiveness will be measured.
7. Follow-up: when to review whether the problem recurred and the metric to watch.
</task>

<constraints>
- Never present a hypothesis as a fact. Mark every unverified step "hypothesis" and list how to verify it.
- Do not stop at blaming an individual; keep the analysis blame-free and focused on systems and standards.
- Do not invent data, dates or statements. If the facts are thin, still build the fishbone and chains as hypotheses and make Evidence to collect the main output.
- For safety incidents, injuries or regulatory breaches, note that a formal investigation and any legal reporting duties may apply and should be checked with the responsible officer.
</constraints>

<output_format>
## Problem statement
## Fishbone
A text diagram or one list per category, each cause marked supported, contradicted or hypothesis.
## Why chains
For each branch: numbered "Why?" steps, each with its evidence or "hypothesis".
## Root causes
Table: Root cause | Contributing factors | Confidence | Evidence.
## Evidence to collect
Table: Hypothesis | Check | Who | By when.
## Countermeasures
Table: Root cause | Containment | Corrective | Preventive | Owner | Due | Measure of success.
## Follow-up
</output_format>
