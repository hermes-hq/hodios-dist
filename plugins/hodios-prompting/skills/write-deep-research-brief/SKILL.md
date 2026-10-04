---
name: write-deep-research-brief
description: Writes a brief for an AI deep-research run - precise question, scope, source rules, output format and how to judge the result - so a research agent investigates the right thing.
license: CC0-1.0
arguments:
  - question
  - purpose
argument-hint: <question> [purpose]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/write-deep-research-brief
  catalog: 2026.1004.2
---

# Write a deep-research brief

## Inputs

- `question` (required): What you want researched, in your own words, however rough.
- `purpose` (optional): Optional - what you will do with the answer, who reads it and when, and what you already know or believe.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Deep-research agents search, read and synthesise many sources over minutes, and they follow the brief literally. A vague brief produces a long, confident report on the wrong question, padded with weak sources. A good brief states the decision the research serves, the exact questions, what is in and out of scope, which sources count and which do not, how to handle conflicting or missing evidence, and the shape of the report. It also tells the reader in advance how to judge whether the run succeeded.

<question>
$question
</question>
Only if purpose was provided: 
<purpose>
$purpose
</purpose>
</context>

<task>
1. Check what is missing for a precise brief: the decision or use, the audience, geography, time period, depth, and any must-cover or must-avoid items. If the gaps would change the research substantially, list up to five clarifying questions first, then write the brief with your best assumptions clearly marked so the user can run it as is or edit it.
2. Write the research brief to be pasted into a research agent:
   - Objective: the decision or purpose in one or two sentences.
   - Main question and three to six sub-questions, each answerable with evidence.
   - Scope: geography, time window, populations, products or sectors in and out; what not to spend time on.
   - Sources: preferred types (primary data, official statistics, peer-reviewed research, regulatory filings, reputable trade press, company documentation), sources to avoid or treat with caution (content farms, undated pages, vendor marketing presented as evidence), a recency requirement, and languages.
   - Evidence rules: cite every factual claim with a link; distinguish established facts, estimates and opinions; report conflicting figures side by side with their sources instead of picking one; say "not found" rather than fill gaps; note the date of every statistic.
   - Output format: an executive summary of a stated length, sections per sub-question, a comparison table if relevant, a confidence rating per finding, open questions, and a full source list.
   - Length and depth: a target length and how many sources are enough.
3. Write how to judge the result: a short checklist the user applies afterwards (every sub-question answered or marked not found; claims cited and spot-checked; sources recent and primary where possible; conflicts surfaced; no conclusions beyond the evidence).
</task>

<constraints>
- Model- and product-agnostic: no references to a specific research tool's features.
- Make sub-questions concrete and evidence-seeking, not "discuss" or "explore".
- Do not answer the research question yourself or seed the brief with claims you cannot source.
- For health, legal or financial research, add to the brief that the output is background reading and that decisions should be checked with a qualified professional.
- Keep the brief under about 450 words so it stays readable and editable.
</constraints>

<output_format>
## Clarifying questions
Numbered, only if needed; otherwise write "None - assumptions are marked in the brief."
## Research brief
One fenced code block, ready to paste, with the labelled parts above and assumptions marked [ASSUMPTION: …].
## How to judge the result
A checklist of five to eight items.
</output_format>
