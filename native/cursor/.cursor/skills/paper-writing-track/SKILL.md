---
name: paper-writing-track
description: Takes a manuscript from target journal and outline through methods and results, introduction and discussion, title and abstract, and a pre-submission check, pausing for approval between steps.
license: CC0-1.0
metadata:
  version: 1.1.0
  kind: workflow
  category: scientific-writing
  source: https://hermes-ide.com/prompts/paper-writing-track
  catalog: 2026.1004.2
---

# Paper writing track

## Inputs

- [STUDY_SUMMARY] (required): The study - question, design, participants or materials, analyses, key results (paste the numbers or tables), sources you plan to cite with notes, and any drafts or notes you already have.
- [TARGET_JOURNAL] (optional): The journal you intend to submit to, with its article type and author guidelines if you have them. If empty, step 1 proposes a shortlist.
- [SLUG] (optional; default: paper): Short kebab-case name for the paper, used for the folder the step artifacts are saved in.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Writes a research paper the way experienced authors do: venue and message first, then methods and results while the numbers are fixed, then the introduction and discussion that frame them, then the title and abstract, and finally a check of the whole manuscript as an editor and reviewer would read it. Each step writes one artifact and stops for approval, and later steps build on the approved artifacts instead of re-asking.

<study>
[STUDY_SUMMARY]
</study>

Only if [TARGET_JOURNAL] was provided: Target journal: [TARGET_JOURNAL]. Follow its article type, word limits and section headings throughout, and say where its guidelines are needed but not supplied.

Rules for every step:
- The data and the author's notes are the only source of results. Never invent numbers, participants, findings, references or quotations; mark gaps as [MISSING: ...] and list them at the end of each artifact.
- Cite only sources the author supplied, by the key or reference they gave. Every other claim that needs support gets [CITE: what the source must show].
- Keep claims proportional to the design: causal language only with a design that supports it, and the same conclusion stated the same way in every section.
- Track word counts against the journal's limits, and keep terminology, abbreviations, group names and numbers identical across sections.
- Remind the author once, at the start, to follow the journal's policy on disclosing AI assistance; the author is responsible for every word submitted.

## Steps

Work through these steps in order. Do not skip a gate.

1. outline (plan)
2. methods-results (build)
3. intro-discussion (build)
4. abstract (build)
5. presubmission (review)

### Step 1: Target journal and outline

Fix the venue, the message and the shape of the paper before drafting anything.

1. If no target journal was given, propose three to five candidates in tiers (reach, realistic, safe) with the reason each fits, marking fees, metrics and timelines as facts to verify, and ask the author to choose. If one was given, extract or ask for its article type, word and display-item limits, required sections, reference style and reporting requirements.
2. Name the reporting guideline that applies to the design (for example CONSORT, STROBE, PRISMA, ARRIVE, COREQ, STARD, TRIPOD) or say that none does.
3. Write the paper's message in one sentence and the two or three supporting findings, and check that the data actually support them.
4. Produce an outline: working title, section headings, the point of each paragraph in one line, and the planned figures and tables with the result each shows.
5. List what is missing from the study summary to write the methods and results.

Stop and wait for approval of the journal, message and outline, and for answers to the missing items.

Save this step's result to `papers/[SLUG]/01-target-and-outline.md`.

**Gate:** stop here and wait for the user's approval before step 2 (methods-results).

### Step 2: Methods and results

Draft the methods and results from the approved outline.

1. Methods: write enough for another researcher to repeat the study, following the reporting guideline from step 1 - design, setting, participants or materials, interventions or exposures, outcomes and measurement, sample size reasoning, randomisation and blinding where relevant, analysis with software versions, missing data, ethics and consent (with placeholders for reference numbers), and data and code availability.
2. Before the results, check the numbers: totals that add up, percentages that match counts, p values consistent with test statistics, intervals containing their estimates. List inconsistencies for the author instead of fixing them silently.
3. Results: report in the order of the questions - flow and sample, primary outcome, secondary outcomes, then sensitivity and exploratory analyses labelled as such - with effect sizes, confidence intervals and exact statistics, figure and table references, and no interpretation. For qualitative studies, report each theme with its definition and verbatim quotes from the author's data.
4. Draft table shells and figure captions for the display items in the outline.
5. End with the reporting-guideline items still missing and every [MISSING] placeholder.

Stop and wait for approval and for corrected numbers before writing the framing sections.

Save this step's result to `papers/[SLUG]/02-methods-results.md`.

**Gate:** stop here and wait for the user's approval before step 3 (intro-discussion).

### Step 3: Introduction and discussion

Frame the approved results.

1. Introduction: follow the field-gap-aim funnel (establish the territory, establish the niche, occupy it). Cite supplied sources only for what the author's notes say they show, and use [CITE: ...] elsewhere. End with aims or hypotheses that match the approved methods exactly. Avoid claims of being first unless the supplied literature supports them.
2. Discussion: open with the main finding answering the question in one or two sentences; interpret it against the supplied literature, including studies that disagree; give mechanisms or explanations as possibilities, not findings; give strengths and limitations honestly, with the likely direction of each bias; state implications for research, practice or policy that the design can support; and close with a conclusion that matches the abstract-level message from step 1.
3. Check consistency: the aim in the introduction, the question answered in the discussion and the conclusion use the same words and claim strength.
4. Produce a citation map: each claim, the source key or placeholder, and whether the author's notes support it.

Stop and wait for approval.

Save this step's result to `papers/[SLUG]/03-introduction-discussion.md`.

**Gate:** stop here and wait for the user's approval before step 4 (abstract).

### Step 4: Title and abstract

Compress the approved paper.

1. Write three title options: one declarative (states the finding), one descriptive (states the question and design), and one that fits the journal's conventions, each within its length limit. Include the design in the title or subtitle when the reporting guideline expects it.
2. Write the abstract in the journal's format (structured headings or unstructured) and word limit: background and gap in one or two sentences, objective, design and participants, main results with the key numbers and intervals exactly as in the results section, and a conclusion no stronger than the discussion.
3. Check every number and claim in the abstract against the approved sections and list any mismatch.
4. Suggest keywords not already in the title, and highlights or a plain-language summary if the journal asks for them.

Stop and wait for approval.

Save this step's result to `papers/[SLUG]/04-title-abstract.md`.

**Gate:** stop here and wait for the user's approval before step 5 (presubmission).

### Step 5: Pre-submission check

Read the assembled manuscript as the handling editor and a reviewer would, then list what to fix.

1. Editor's desk check: fit with the journal's scope and article type, word and display-item limits, required sections and statements (ethics, consent, funding, conflicts of interest, data availability, author contributions, AI-use disclosure), reference style, and figure file requirements.
2. Reviewer's read: the three most likely major criticisms and what would pre-empt each, in text the author can add.
3. Reporting guideline: go through the checklist named in step 1 and list items missing with where to add them.
4. Consistency: numbers identical across abstract, text, tables and figures; abbreviations defined once; terms and group names consistent; every figure and table cited in order.
5. References: every [CITE] and [MISSING] placeholder still open, and a reminder to verify that each reference exists and supports its claim before submission.
6. Give a final submission checklist, including a pointer to drafting the cover letter.

Say that this check does not guarantee acceptance and that a colleague outside the project is the best final reader.

Save this step's result to `papers/[SLUG]/05-presubmission-check.md`.
