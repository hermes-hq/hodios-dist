---
description: Writes a constructive manuscript review with a summary, major and minor issues, methodological and reporting concerns, and a reasoned recommendation. Use when refereeing a paper.
---

# Write a peer review

## Inputs

- [MANUSCRIPT] (required): The manuscript text, including methods, results, tables and supplementary material you were sent.
- [VENUE] (optional): The journal or conference and its article type, so the review matches its scope and standards.
- [FOCUS] (optional): Anything the editor asked you to concentrate on, or your own area of expertise, for example "the statistical analysis".

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
Editors value reviews that show the reviewer understood the paper, separate fatal problems from fixable ones, explain why each issue matters, and say what would resolve it. Authors value reviews that are specific and respectful. Weak reviews are vague ("the methods are unclear"), demand a different study, insist on citing the reviewer's own work, or nitpick style while missing a design flaw. Peer-review manuscripts are confidential, and many publishers restrict uploading them to AI tools, so the reviewer remains responsible for following the venue's policy and for every judgement in the report.
</context>

<task>
Review this manuscriptOnly if [VENUE] was provided:  submitted to [VENUE]:
<manuscript>
[MANUSCRIPT]
</manuscript>
Only if [FOCUS] was provided: 
Give extra attention to: [FOCUS]

1. Before judging, summarise the paper's question, design, main findings and claimed contribution in your own words.
2. Assess whether the question matters and whether the contribution is new, judging only from what the manuscript itself shows and cites.
3. Check the methods against the question: design, sample and power, measures, controls, analysis choices, handling of missing data and multiple comparisons, and whether the conclusions follow from the results. Name the reporting guideline that applies (for example CONSORT, STROBE, PRISMA, ARRIVE, COREQ, TRIPOD) and note the important items missing.
4. Check reproducibility: availability of data, code and materials, and whether the methods are described well enough to repeat.
5. Sort issues into major (could change the conclusions or the decision) and minor (clarity, presentation, small analyses). For each major issue give the location, the problem, why it matters and what would resolve it.
6. Make a recommendation (accept, minor revision, major revision or reject) that follows from the major issues.
</task>

<constraints>
- Every issue points to a specific section, table, figure or line and proposes a resolution. No vague criticism.
- Stay within the paper's aims: do not ask for a different study, and request new experiments or data only when the conclusions cannot stand without them.
- Do not ask the authors to cite particular papers unless a missing citation is needed for a specific claim, and never suggest references you cannot verify.
- Be respectful and impersonal: critique the work, never the authors. Acknowledge real strengths.
- Do not speculate about the authors' identity or intentions. Raise suspected misconduct (duplicated images, impossible numbers, plagiarism) only in the confidential comments, with the evidence.
- If the text provided is only part of the manuscript, say so and limit the review to what you can see.
- Start the report with one line reminding the reviewer to check that the venue permits AI assistance and to keep the manuscript confidential.
</constraints>

<output_format>
One reminder line, then:
## Summary
One paragraph.
## Overall assessment
Strengths and the main concerns in three to five sentences.
## Major issues
Numbered: location — problem — why it matters — what would resolve it.
## Minor issues
Numbered, one or two lines each.
## Reporting and reproducibility
The guideline that applies, missing items, and data and code availability.
## Recommendation
The recommendation and the two or three reasons that decide it.
## Confidential comments to the editor
Anything not for the authors, or "None".
</output_format>

Arguments: $ARGUMENTS
