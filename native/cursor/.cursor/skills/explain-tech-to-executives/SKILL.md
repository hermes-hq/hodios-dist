---
name: explain-tech-to-executives
description: Translates a technical issue or decision into a one-page executive brief with business impact, options, cost, risk and the specific ask. Use when leadership must decide or fund something technical.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: writing
  source: https://hermes-ide.com/prompts/explain-tech-to-executives
  catalog: 2026.1004.3
---

# Explain a technical issue to executives

## Inputs

- [TECHNICAL_DETAIL] (required): The technical issue, incident, proposal or decision in your own words, with any numbers you have (cost, incidents, customers affected, timelines).
- [AUDIENCE] (optional; default: executive team): Who reads the brief, for example "CEO and CFO", "board", "VP Sales".
- [DECISION_NEEDED] (optional): What you need from them, for example approval, budget, a trade-off between scope and date, or just awareness.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Executives decide among options under constraints of money, time, risk and customers. They do not need to understand the mechanism, but they do need to trust that the engineer understands it and has framed the choice honestly. Technical briefs fail when the ask is buried at the end, when impact is expressed in technical units (CPU, latency, story points) instead of customers, revenue, risk or dates, when only one option is offered, or when uncertainty is either hidden or so heavily hedged that no decision is possible.
</context>

<task>
Write a brief for [AUDIENCE] about:
[TECHNICAL_DETAIL]
Only if [DECISION_NEEDED] was provided: What is needed from them: [DECISION_NEEDED]
If what you need from them is not stated and cannot be inferred, ask; a brief without an ask is a status update, so say so if that is what it is.

1. Lead with the ask: the decision, by when, and the recommended answer, in two sentences.
2. Explain the situation in business terms: who or what is affected (customers, revenue, compliance, delivery dates, team capacity), how much, and what happens if nothing is done, with a time frame. Use an analogy only if it is accurate.
3. Give two or three options, including doing nothing. For each: what it costs (money, people, time), what it delivers, what it puts at risk, and what it gives up.
4. Give the recommendation and the main reason, plus the signal that would tell them it is working.
5. Translate every technical term into its consequence, or drop it. Keep one technical sentence at most, for credibility, in plain words.
6. Separate known facts from estimates. Express uncertainty as a range or a confidence level, once.
</task>

<constraints>
- At most one page (about 300 to 400 words) for the brief.
- Use only numbers from the input. Where a number the audience will expect is missing (cost, customers affected, date), mark it `[need: …]` rather than inventing it.
- Neutral, factual tone: no alarmism, no reassurance the facts do not support, no blame.
- Lead with the answer. Add reasoning only where it changes what the reader will do.
- No preamble, no restating the request and no closing summary on a short answer.
</constraints>

<output_format>
## Brief
Subject line, then sections: The ask, What is happening, Options (a short table: Option | Cost | Time | Risk | What we give up), Recommendation, What we will report back and when.
## Glossary removed
Bullets: technical terms from the input you translated or dropped, and what replaced them, so the author can check nothing was lost.
## Gaps
Bullets: each `[need: …]` placeholder and the question an executive is likely to ask that the brief cannot yet answer.
</output_format>
