---
name: summarize-book
description: Summarises a non-fiction book's argument, key ideas, evidence and critiques, and turns it into actions for your purpose. Says when it does not know the book instead of inventing content.
license: CC0-1.0
arguments:
  - book
  - purpose
argument-hint: <book> [purpose]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: summarization
  source: https://hermes-ide.com/prompts/summarize-book
  catalog: 2026.1003.2
---

# Summarise a book

## Inputs

- `book` (required): The book's title and author, or your notes, highlights or chapter text from it.
- `purpose` (optional): Optional - why you are reading it and what you want to apply it to.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
The reader wants to understand what a book argues, how well it argues it, and what to do with it, not a chapter-by-chapter recap. The biggest risk is a confident summary of a book you do not actually know well: invented chapters, quotes or studies are worse than no summary.

<book>
$book
</book>
Only if purpose was provided: 
<purpose>
$purpose
</purpose>
</context>

<task>
1. Decide what you are working from. If the input is the user's notes or text, summarise only that and say so. If it is a title, judge honestly how well you know the book. If you do not recognise it, or know only its reputation, say so, offer what you can say with confidence, and ask the user to paste notes or a table of contents. Do not produce the full summary from guesses.
2. State the thesis in one or two sentences: the claim the author wants the reader to accept.
3. Lay out the core argument as a short chain: the problem, the author's diagnosis, the proposed answer, and why the author thinks it works.
4. Explain five to eight key ideas, each in plain words with an example of how it shows up in real life.
5. Describe the evidence the author relies on (research, case studies, personal experience, history) and how strong it is.
6. Give the main critiques and limits: where findings have not held up, where the argument overreaches, and who the advice fits less well. Attribute criticism to its general source ("later replication attempts", "reviewers in the field") rather than inventing names.
7. Turn it into three to five concrete actions for the user's purpose, or for a general reader if no purpose is given.
8. Say who should read it in full and which chapters, if you know them, give the most value.
</task>

<constraints>
- No direct quotes unless they appear in the user's own notes. Paraphrase instead.
- Do not invent chapter titles, page numbers, studies, statistics or anecdotes. If unsure of a detail, leave it out or mark it "(verify)".
- Separate what the author claims from what is well established.
- For fiction, adapt: replace argument and evidence with premise, themes, characters and craft, and avoid spoilers unless the user asks.
- Aim for a summary readable in five minutes.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Start with one line: "Working from: your notes" or "Working from: my general knowledge of the book (confidence: high, medium or low)".
## In one paragraph
## The core argument
A numbered chain of three to five steps.
## Key ideas
Numbered: idea in bold, then two or three sentences and an example.
## Evidence
## Critiques and limits
## Apply it
Checklist of three to five actions tied to the purpose.
## Read it in full if
</output_format>
