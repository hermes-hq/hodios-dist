---
name: respond-to-reviewers
description: Drafts a point-by-point response to peer-review comments, giving the change made or a polite, evidenced rebuttal for each, never claiming unmade changes. Use for revise-and-resubmit.
license: CC0-1.0
arguments:
  - reviews
  - manuscript_changes
argument-hint: <reviews> [manuscript_changes]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/respond-to-reviewers
  catalog: 2026.1002.0
---

# Respond to peer reviewers

## Inputs

- `reviews` (required): The decision letter and all reviewer comments, pasted in full.
- `manuscript_changes` (optional): What you changed or plan to change, and where (page, line or section); also any points you disagree with and why.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Editors read the response letter to decide whether the authors took the reviews seriously, and reviewers check that every point was answered and that each answer matches the revised manuscript. Good responses quote each comment, answer it directly, say exactly what changed and where, and disagree only with evidence and courtesy. Letters fail when they skip or merge points, are defensive, thank the reviewer in every line, or claim changes that are not in the manuscript.
</context>

<task>
Draft a response to these reviews:
<reviews>
$reviews
</reviews>
Only if manuscript_changes was provided: 
Changes made or planned, and the authors' positions:
<changes>
$manuscript_changes
</changes>

1. Split the reviews into individual comments, numbered by reviewer (R1.1, R1.2, R2.1…), and split multi-part comments into separate points. Include the editor's own requests as E.1, E.2.
2. Triage each comment: type (major, minor, clarification, typo), proposed action (accept, partially accept, rebut), and effort (low, medium, high).
3. For each comment, write the response: a direct answer in the first sentence, then the change made with its location, or, for a rebuttal, the reason with evidence (data, analysis, citations from the authors' material), and any concession or compromise offered.
4. Where reviewers conflict, say so to the editor and explain which way you went and why.
5. Write a short opening paragraph to the editor summarising the main changes.
</task>

<constraints>
- Claim a change only if it appears in the authors' changes. Where you have no information, write a proposed response marked "[AUTHOR TO CONFIRM: proposed change …]" so nothing is promised by accident.
- Quote every reviewer comment verbatim; never paraphrase it in a way that changes its meaning, and never leave one out.
- Do not invent analyses, results, references or page numbers. Use "[page/line]" placeholders.
- Be courteous and specific. Thank the reviewers once in the opening, not in every response. Concede valid points plainly. Never be sarcastic, never question the reviewer's competence.
- A rebuttal needs a reason a reasonable reviewer could accept. If the only reason is effort, say so honestly and offer a limitation statement instead.
</constraints>

<output_format>
## Triage
A table: ID | summary of the comment (under 12 words) | type | action | effort.
## Response letter
The opening paragraph to the editor, then for each comment:
**R1.1** > the reviewer's comment, quoted
**Response:** the answer.
**Change:** what changed and where, or "No change" with the reason.
## Open items
A checklist of every "[AUTHOR TO CONFIRM]" and placeholder, plus any comment that needs new analysis or data.
</output_format>
