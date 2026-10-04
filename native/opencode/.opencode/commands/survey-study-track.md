---
description: Runs a survey study in gated steps from research questions and hypotheses to questionnaire, pilot, sampling and fielding, cleaning, analysis and reporting, checking each stage before the next.
---

# Survey study track

## Inputs

- [TOPIC] (required): What the survey is about and why, for example "how first-generation students use campus support services".
- [POPULATION] (required): Who the results should describe, and how you can reach them (a list, a panel, a platform, an organisation).
- [TIMELINE_WEEKS] (optional; default: 12): Weeks available from planning to the final report.

Read each value from the arguments below. If a required value is missing, ask for it once.

Runs a survey study on [TOPIC] among [POPULATION] within [TIMELINE_WEEKS] weeks. Each step produces one artifact and stops for approval; later steps build on approved artifacts instead of re-asking.

Rules for every step: never invent responses, response rates or results; work only from material and output the user supplies, and when you cannot run an analysis, give the exact code or spreadsheet steps and continue from the pasted output. Keep a running decision log (what was decided, when, why) so the report can state it. Fix the analysis plan and exclusion rules before data arrive, and label anything decided after seeing data as exploratory. Name ethics review and consent as items for the user's institution to confirm. If the user asks to skip a gate, confirm once that later steps will build on unreviewed choices, then continue and note the skipped gate in the log.

## Steps

Work through these steps in order. Do not skip a gate.

1. questions (plan)
2. questionnaire (design)
3. pilot (verify)
4. fielding (build)
5. cleaning (verify)
6. report (ship)

### Step 1: Research questions, hypotheses and plan

1. State the decision or knowledge gap the survey serves, and why a survey (not interviews, records or an experiment) is the right method. Say so if it is not.
2. Write one primary and up to three secondary research questions, with hypotheses where the study is confirmatory.
3. List the constructs to measure, each with a definition and whether a validated scale exists to look for.
4. Sketch the analysis for each question: the comparison, the key variables and the minimum sample per group it needs.
5. Lay out the [TIMELINE_WEEKS]-week schedule across the six steps, and note ethics review and data protection checks to start now.

Write sections: Purpose, Questions and hypotheses, Constructs, Analysis sketch, Schedule. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 2 (questionnaire).

### Step 2: Questionnaire

From the approved constructs, draft the instrument.

1. Map every question to a construct and research question; drop questions that map to none.
2. Use validated scales where they exist (name them as candidates to check for licence and validity in this population); write new items only for gaps.
3. Write neutral, single-barrelled items with balanced response options, a "prefer not to say" where needed, and consistent scale direction, marking any reverse-coded items.
4. Order from easy to sensitive, put demographics at the end, add skip logic, and include one attention or quality check if the sample source calls for it.
5. Draft the consent text and estimate completion time.

Write sections: Construct map (table), Questionnaire, Consent text, Estimated time. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 3 (pilot).

### Step 3: Pilot

1. Plan cognitive interviews with three to five people from [POPULATION]: think-aloud and probes for the items most likely to be misread.
2. Plan a small soft launch to test the survey link, skip logic, timing, the export and drop-off points.
3. When the user pastes pilot notes or soft-launch data, list each problem found, its fix, and the revised items.

Write sections: Pilot plan, Findings (only from what the user reports), Revisions. Stop and wait for approval of the final questionnaire.

**Gate:** stop here and wait for the user's approval before step 4 (fielding).

### Step 4: Sampling and fielding

1. Define the sampling frame and its gaps against [POPULATION], the sampling method, and the target sample size from the step 1 analysis sketch, with the expected response rate stated as an assumption.
2. Plan distribution: channels, invitation and reminder schedule (dates and wording), incentives if any, and how duplicate or fraudulent responses are prevented.
3. Set monitoring checks during fielding: responses per day, completion rate, drop-off by page, and representativeness against known population figures.
4. Write the pre-registered exclusion rules and the cleaning plan now, before data arrive.

Write sections: Sample, Distribution plan, Monitoring, Exclusion rules. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 5 (cleaning).

### Step 5: Cleaning

Work on a copy of the raw export, never the original.

1. Remove test and preview responses, then apply the approved exclusion rules in order (incomplete, failed checks, speeders, straight-lining, duplicates) and count what each removes.
2. Recode: reverse-coded items, scale labels to numbers, "don't know" and "prefer not to say" to missing (never to a midpoint), multi-select into indicator columns.
3. Build scale scores and report reliability; tidy and code open text.
4. Produce a codebook and a flow of counts from invited to analysed.

Write sections: Exclusion flow (table), Recoding log, Codebook, Data issues. Report only counts from data or output you actually saw. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 6 (report).

### Step 6: Analysis and report

1. Run the analysis from step 1 on the cleaned data: descriptives with counts behind every percentage, then the planned comparisons with effect sizes and uncertainty (and weighting if planned).
2. Answer each research question in order; keep exploratory findings in a separate, labelled section.
3. State the limits: coverage and non-response bias, self-report, and what the sample can and cannot represent.
4. Write the report: key findings first, method in brief, results by question, limitations, and an appendix with the questionnaire, codebook, exclusion flow and decision log.

Use only numbers from the cleaned data or output the user supplied.

Arguments: $ARGUMENTS
