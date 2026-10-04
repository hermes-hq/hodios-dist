Produces a finished docx report that answers a real question for managers who will act on it, not analysts, where every number can be traced to the script that computed it. Reports built by hand drift: a number pasted from an old run, a chart from a different filter, a finding the data does not support. This track pins down the question first, keeps all computation in a script that writes its results to a file, drafts findings that cite those results, pauses for review, and only then builds the file.

Rules for every step:
- Every number in the report comes from the results file written by the analysis script. No number is typed by hand, rounded differently in different places, or recalled from memory.
- Use the language and libraries already in the project; otherwise use Python with standard data and document libraries.
- Claim only what the analysis shows. Correlation is not presented as cause; small samples, missing data and excluded rows are stated where they affect a finding.
- Do not send, upload or share the report anywhere. Write it to the project.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.

## Steps

Work through these steps in order. Do not skip a gate.

1. question (plan)
2. analysis (build)
3. findings (review)
4. export (ship)

### Step 1: Pin down the question

<question>
[QUESTION]
</question>

1. Restate the question as the decision it informs and the answer that would change that decision ("If churn in the new plan is higher than in the old one by more than X, revert pricing").
2. Define every metric precisely: numerator, denominator, filters, time window, grain, and how missing data counts.
3. Inspect the data at `[DATA_PATH]`: columns, row counts, date range, grain and known quality issues. Check that it can answer the question; if it cannot, say what is missing.
4. Plan the analysis: the comparisons, breakdowns and checks needed, and the charts (one per finding the decision needs, at most about six).
5. List assumptions and the questions for the requester.

Write the artifact: Decision, Metric definitions, Data fit, Analysis plan, Planned charts, Assumptions, Open questions. Stop and wait for approval.

Save this step's result to `report-build/01-question.md`.

**Gate:** stop here and wait for the user's approval before step 2 (analysis).

### Step 2: Script the analysis and charts

1. Write one analysis script (or a small module) that loads the data read-only, applies the approved definitions, and computes every number the report will use.
2. Write all results to one machine-readable results file (JSON or CSV), each value with a stable key, its definition, the filter used and the row count behind it.
3. Run sanity checks in the script: totals reconcile with the source, subgroup counts sum to the total, no unexpected nulls in metric inputs, date ranges as approved. Fail loudly when one does not hold.
4. Generate each planned chart from the same results, saved as image files (and as native chart data if the output is a deck). Each chart has a title that states the finding, labelled axes with units, a zero baseline for bar charts, colour-blind-safe colours, and a source note.
5. Run the script from scratch and confirm it reproduces the same results file.

Continue to step 3.

### Step 3: Draft findings for review

1. Write the report text for managers who will act on it, not analysts: a summary answering the question in two or three sentences, then one section per finding (the claim, the evidence, what it means for the decision), caveats, and a short method note.
2. Tag every number in the draft with its key from the results file, for example `[churn_rate_new_plan]`, so it can be checked and filled automatically.
3. State uncertainty where it matters: sample sizes, intervals or ranges if computed, data gaps, and what the analysis cannot tell.
4. Recommend only what follows from the findings; label anything beyond them as a suggestion to test.

Write the artifact with the draft and the list of charts it uses. Stop and wait for review before export; the reviewer's changes to wording or emphasis must not introduce numbers that are not in the results file.

Save this step's result to `report-build/03-findings.md`.

**Gate:** stop here and wait for the user's approval before step 4 (export).

### Step 4: Export the docx file

1. Build the file with a script, not by hand: fill the approved text, replacing every results key with its value formatted consistently (same rounding and units throughout), and insert the charts with captions and alt text.
2. Use the project's report template or brand styles if they exist; otherwise a clean default with headings, page numbers or slide numbers, and a source and method appendix.
3. Check the built file automatically: no unreplaced keys remain, every number in the file matches the results file, every chart referenced is present, and the file opens again in the library that wrote it. Convert to PDF or images with a local office suite if available and look at each page or slide for overflow and layout problems.
4. Save the analysis script, results file, charts and report together with a short README saying how to rebuild everything.

Write the report log: Files written, Rebuild command, Checks run with real results, Changes made after review, Known limitations.

Save this step's result to `report-build/04-report-log.md`.
