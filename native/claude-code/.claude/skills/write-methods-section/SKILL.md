---
name: write-methods-section
description: Writes a manuscript methods section another researcher could replicate, following the relevant reporting guideline and flagging every missing detail. For authors drafting a paper or thesis.
license: CC0-1.0
arguments:
  - study_details
  - reporting_guideline
  - word_limit
argument-hint: <study_details> [reporting_guideline] [word_limit]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/write-methods-section
  catalog: 2026.1002.2
---

# Write a replicable methods section

## Inputs

- `study_details` (required): Everything about how the study was done - design, setting, dates, participants or materials, procedures, measures, sample size, analysis and software, ethics approval and registration. Notes, protocol text or a rough draft all work.
- `reporting_guideline` (optional): The guideline to follow, for example CONSORT, STROBE, PRISMA, ARRIVE, COREQ, SRQR, STARD or TRIPOD. Leave empty to have one chosen from the design.
- `word_limit` (optional): The journal's limit for the methods section, if any, for example "1,500 words" or "no limit, details may go to supplementary material".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
The methods section exists so readers can judge the results and repeat the study. It fails when it describes what was intended rather than what was done, leaves out decisions that shape results (eligibility, randomisation, exclusions, deviations from protocol, how missing data were handled, software versions), or hides them in vague phrases such as "standard procedures" and "appropriate statistical tests". Reporting guidelines collected by the EQUATOR Network list what readers need for each design: CONSORT for randomised trials, STROBE for observational studies, PRISMA for systematic reviews, ARRIVE for animal research, COREQ or SRQR for qualitative research, STARD for diagnostic accuracy, TRIPOD for prediction models, and others.
</context>

<task>
Write the methods section from these details.
<study_details>
$study_details
</study_details>
Only if reporting_guideline was provided: Reporting guideline: $reporting_guideline
Only if word_limit was provided: Word limit: $word_limit

1. Identify the design and confirm the reporting guideline. If none was given, choose it from the design and say why; if the given guideline does not fit the design, say so and suggest the right one.
2. Organise the section with the subheadings readers expect for this design and guideline, for example: study design and setting; participants (eligibility, recruitment, dates); interventions or exposures; outcomes and measures (with how and when measured, and validity of instruments); sample size; randomisation and blinding where relevant; data collection; statistical or qualitative analysis; ethics and registration.
3. Write in the past tense and describe what was done, with enough detail to replicate: quantities, units, timings, versions of software and instruments, model specifications, thresholds and the handling of missing data and outliers. Cite the method for standard techniques rather than re-describe them, using the citation the user provided or a [CITE: method] placeholder.
4. Wherever a detail the guideline requires is missing, insert [GAP: what is needed] in the text and list it under Gaps to fill with the guideline item it serves.
5. Keep within the word limit by moving long procedural detail to supplementary material, and list what moved.
</task>

<constraints>
- Use only the details provided. Never invent sample sizes, dates, approval numbers, registration IDs, software versions, effect sizes or procedures. Every unknown becomes a [GAP: …] marker.
- Report what was done, not what was planned. If the details mention a protocol deviation, report it plainly.
- Do not put results in the methods (except participant flow if the guideline places it there).
- Paraphrase guideline items in your own words and tell the user to check the official checklist for the current version.
- Use the terms and abbreviations the user uses, defining each abbreviation once.
</constraints>

<output_format>
## Guideline used
One line with the guideline and why.
## Methods
The section, with the subheadings and [GAP: …] markers in place.
## Gaps to fill
Table: gap | guideline item it serves | why reviewers will ask for it.
## Moved to supplementary material
Bullets, or "Nothing moved".
</output_format>
