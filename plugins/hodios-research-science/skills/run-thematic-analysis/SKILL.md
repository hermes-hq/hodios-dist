---
name: run-thematic-analysis
description: Runs reflexive thematic analysis on qualitative data through familiarisation, initial codes, candidate themes with quotes, review and definitions. For qualitative researchers.
license: CC0-1.0
arguments:
  - data
  - research_question
  - orientation
argument-hint: <data> <research_question> [orientation]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: research-methods
  source: https://hermes-ide.com/prompts/run-thematic-analysis
  catalog: 2026.1003.0
---

# Run a reflexive thematic analysis

## Inputs

- `data` (required): The qualitative data - interview or focus-group transcripts, open survey answers or field notes, with participant IDs. Remove names and identifying details before pasting.
- `research_question` (required): The research question the analysis should answer.
- `orientation` (optional; one of: inductive, deductive; default: inductive): Inductive builds codes from the data; deductive starts from a theory or framework you name in the research question.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Reflexive thematic analysis, as described by Braun and Clarke, moves through six recursive phases: familiarisation, coding, generating initial themes, developing and reviewing themes, refining, defining and naming themes, and writing up. A theme is a pattern of shared meaning organised around a central idea, not a topic summary ("participants talked about money") and not a list of everything said about a question. Codes can be semantic (what is said) or latent (the assumptions underneath). Reflexive TA treats the researcher's interpretation as the analytic resource, so it does not use inter-rater reliability or claim that themes "emerged" from the data. An assistant can speed up coding and suggest patterns, but the analysis is only credible when the researcher checks every quote, revises the themes and owns the interpretation.
</context>

<task>
Run a $orientation reflexive thematic analysis for this question:
<research_question>
$research_question
</research_question>
<data>
$data
</data>

1. **Familiarisation:** note first impressions per participant or source, and patterns or contradictions that stand out across them, as short memos.
2. **Initial codes:** code the data systematically. Give each code a short label, say whether it is mostly semantic or latent, and list the data extracts it applies to by participant ID with a short verbatim quote. Code for the research question; ignore material that is irrelevant to it.
3. **Candidate themes:** cluster codes into three to six candidate themes, each with a central organising concept stated as a claim (not a topic), the codes it brings together, and two or three of the strongest supporting quotes from different participants.
4. **Theme review:** check each theme against the coded extracts and the whole data set. Is it coherent, distinct from the others, supported across participants rather than one voice, and relevant to the question? Merge, split or drop themes as needed and say what changed. Record contradictions and negative cases rather than hide them.
5. **Thematic map:** show themes, any subthemes and how they relate, as a nested list.
6. **Theme definitions:** a name that captures the essence, a definition of two to four sentences of what the theme is and is not, and how it answers the research question.
7. **Notes for the researcher:** where your interpretation is weakest, what to reread, and reflexivity questions to consider about how their own position might shape the analysis.
</task>

<constraints>
- Quote verbatim only, with the participant ID. Never paraphrase inside quotation marks, combine quotes, or invent one. If you cannot find a quote for a claim, drop the claim.
- Report how widespread a pattern is in words that reflect the data ("most participants", "two of eight") and do not turn it into percentages or claims of statistical prevalence.
- Do not report inter-rater reliability or say themes "emerged"; themes are constructed through analysis.
- Keep the participants' language visible, and do not smooth over disagreement.
- If the data still contain names or identifying details, say so at the top and recommend removing them before further analysis.
- If there is too much data to code carefully in one reply, code the first part, say where you stopped, and ask for the rest; do not skim.
- Label this as a first-pass analysis for the researcher to revise.
</constraints>

<output_format>
Use the contract's section headings in order. Initial codes as a table: code | semantic or latent | participants | example quote. Candidate themes as headed blocks. Theme review as a short list of changes. Thematic map as a nested bullet list. Theme definitions as headed paragraphs.
</output_format>
