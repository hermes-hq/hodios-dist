---
name: write-meta-review
description: Writes an editor or area-chair meta-review that synthesises referee reports, resolves disagreements on the merits, states the decision rationale and lists required and optional changes.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: peer-review
  source: https://hermes-ide.com/prompts/write-meta-review
  catalog: 2026.1003.2
---

# Write an editor or area-chair meta-review

## Inputs

- [REVIEWS] (required): The referee reports (anonymised as Reviewer 1, 2, 3), their scores or recommendations, any author response or discussion, and a short summary of the submission.
- [VENUE_CRITERIA] (optional): The venue's review criteria, decision options and meta-review template, for example a conference with accept or reject on soundness, significance and clarity, or a journal with accept, minor, major or reject.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A meta-review is not an average of scores. The editor or area chair weighs the arguments, decides which concerns are valid and decisive, resolves disagreements by reasoning about the evidence and the reviewers' expertise, and explains the decision so authors know what would change it. Weak meta-reviews restate each review in turn, count votes, introduce new objections without saying so, or leave authors unsure what to do. Good ones are short, specific, fair to authors and reviewers, and consistent with the venue's criteria. Review material is confidential, and some venues restrict the use of AI tools with it.
</context>

<task>
Write the meta-review.
<reviews>
[REVIEWS]
</reviews>
Only if [VENUE_CRITERIA] was provided: 
<venue_criteria>
[VENUE_CRITERIA]
</venue_criteria>

1. Summarise the submission and its claimed contribution in two or three sentences.
2. Identify the points of consensus: strengths and concerns raised by more than one reviewer or uncontested.
3. Identify the disagreements. For each, state both positions, weigh them on the merits (is the concern supported by the paper's content, did the author response address it, which reviewer has the relevant expertise or engaged more closely), and say how you resolve it and why.
4. Separate decisive issues (would change the decision) from secondary ones.
5. Recommend a decision using the venue's options, and give the rationale in terms of the venue's criteria. If the reviews do not support a clear decision, state the options and what would tip the balance.
6. List the required changes for acceptance and the optional suggestions, each traceable to a reviewer or marked as the meta-reviewer's own.
7. Note anything the editor or programme chairs should know confidentially: a review that is unprofessional, superficial or shows a possible conflict of interest, or suspected misconduct with the evidence.
</task>

<constraints>
- Base the decision on the arguments in the reviews and the paper's content as described, not on score averages.
- Mark any new concern you raise as your own; do not attribute it to reviewers.
- Do not reveal reviewer identities or speculate about authors' identities.
- Do not let personal or irrelevant factors (the authors' reputation, prior disputes) influence the recommendation; if the user asks for that, decline and explain briefly.
- Keep the tone respectful and impersonal. Disregard or downweight hostile or unsupported remarks, and say so in the confidential note rather than repeating them to authors.
- Start with one line reminding the user to check that the venue allows AI assistance with confidential review material.
</constraints>

<output_format>
One reminder line, then:
## Meta-review
Summary, consensus, disagreements and their resolution, decision and rationale, in 250 to 450 words unless the venue template says otherwise.
## Required changes
Numbered, with source (R1, R2, AC).
## Suggested changes
Numbered, with source.
## Note to the editor or programme chairs
Confidential points, or "None".
</output_format>
