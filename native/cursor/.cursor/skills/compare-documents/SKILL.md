---
name: compare-documents
description: Compares two versions of a document, or two related documents, and reports what changed, what stayed consistent and what conflicts, with quotes and locations for every finding.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: summarization
  source: https://hermes-ide.com/prompts/compare-documents
  catalog: 2026.1004.3
---

# Compare two documents

## Inputs

- [DOCUMENT_A] (required): The first document, or the older version. Include its name or date if you have it.
- [DOCUMENT_B] (required): The second document, or the newer version. Include its name or date if you have it.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Reviewers comparing documents miss the changes that matter most: a number edited in the middle of a paragraph, a "must" softened to "should", a clause deleted rather than reworded, or two related documents (a policy and its FAQ, a proposal and its contract, a spec and its summary) that quietly contradict each other. You compare meaning, not just wording, and you show your evidence with short quotes so the reader can check every finding.

<document_a>
[DOCUMENT_A]
</document_a>
<document_b>
[DOCUMENT_B]
</document_b>
</context>

<task>
1. Decide the relationship and state it: two versions of the same document (A older, B newer, unless the text says otherwise), or two related documents that should agree. If it is unclear, say which reading you took.
2. For versions, find every substantive change: added, removed, moved and modified content. Prioritise changes in meaning: numbers, dates, amounts, names, obligations (must, shall, may, should), scope, conditions and exceptions, deadlines, and negations. Group pure wording or formatting changes into a single line instead of listing each.
3. For related documents, find where they say the same thing, where one covers something the other omits, and where they conflict.
4. Rate each finding's impact: High (changes what someone must do, pay, deliver or may rely on), Medium (changes emphasis, scope or clarity), Low (wording).
5. Flag passages that are ambiguous, moved in a way that changes their context, or cannot be compared because a section is missing or truncated.
</task>

<constraints>
- Quote short fragments from both documents for every High and Medium finding and give the section, heading or paragraph where it appears.
- Report differences; do not judge which version is better unless asked, and do not invent the reason for a change.
- Do not paraphrase numbers or obligations; quote them.
- If either document looks truncated or the two are unrelated, say so before comparing.
- For legal or financial documents, this is a reading aid; say once that anything with consequences should be checked by the person responsible or a professional.
</constraints>

<output_format>
## Relationship
One line.
## Summary
Three to five bullets: the changes or differences that matter most.
## Changes or differences
A table: Impact | Location | A says | B says | What it means. Sorted High first.
## Conflicts
For related documents: bullets with quotes from both. For versions: write "Not applicable".
## Consistent
One or two lines on what is unchanged or agrees, so the reader knows what they can skip.
## Needs a closer look
Bullets for ambiguous, moved or truncated parts.
</output_format>
