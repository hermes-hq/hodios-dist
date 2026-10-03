---
name: novel-revision-track
description: Revises a finished novel draft in gated passes from big to small (read-through notes, structural edit, scene pass, line pass, beta-reader brief), stopping for your approval each time.
license: CC0-1.0
arguments:
  - manuscript_summary
  - author_goals
argument-hint: <manuscript_summary> [author_goals]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: workflow
  category: fiction
  source: https://hermes-ide.com/prompts/novel-revision-track
  catalog: 2026.1003.2
---

# Novel revision track

## Inputs

- `manuscript_summary` (required): Title, genre, word count, a chapter-by-chapter summary (a line or two each) and what you already think is wrong. You will paste chapters when a step asks for them.
- `author_goals` (optional): What this revision must achieve (tighten pacing, fix the middle, ready for agents, ready to self-publish), your deadline and anything that must not change. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Revises a finished novel draft the way a professional editor sequences the work: biggest problems first, because polishing sentences in a chapter that will be cut wastes weeks. The track works from the manuscript summary and goals below, plus the chapters the author pastes when a step asks for them.

<manuscript_summary>
$manuscript_summary
</manuscript_summary>
Only if author_goals was provided: 
<author_goals>
$author_goals
</author_goals>

Rules for every step: the book belongs to the author, so diagnose and offer options, rewriting only small samples where a step says so; never contradict an approved step without flagging it; base claims only on what the author has pasted or summarised, and say "I have not seen this chapter" instead of guessing; keep each document readable in ten minutes. If the author wants to skip to line edits, explain in one line why structure comes first, offer to run the structural step on the summary alone, and keep every gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. read-through (review)
2. structure (review)
3. scenes (build)
4. lines (build)
5. beta-brief (verify)

### Step 1: Read-through notes

Build an honest picture of the whole book before changing anything.

1. If the summary lacks a chapter outline (grouped ranges are fine), the genre or the word count, ask for them and stop. Otherwise write these notes from the summary now, and ask for the first, a middle and the final chapter to test them: openings, middles and endings fail in different ways.
2. From the summary and pasted chapters, say what the book is about in one sentence (story and theme), what the opening promises the reader, and whether the ending keeps that promise.
3. Map the shape: where the inciting incident, the first-act turn, the midpoint, the crisis and the climax fall, as a percentage of the book. Compare with what the genre and length usually need and flag large drifts.
4. Note the five biggest strengths to protect in revision.
5. Note the five biggest problems, in order of impact on the reader (for example a passive protagonist in act two, a subplot that never pays off, an ending resolved by coincidence). For each, give the evidence (chapter, summary line or quoted passage).
6. Check the problems against the author's goals and say which ones the goals require fixing now.

Write the document with sections One-sentence book, Shape, Strengths to protect, Biggest problems, What the goals require.

Stop and wait for the author to agree, disagree or reorder the problems before planning the structural edit.

Save this step's result to `revision/01-read-through-notes.md`.

**Gate:** stop here and wait for the user's approval before step 2 (structure).

### Step 2: Structural edit

Plan the large changes the approved problem list calls for. Nothing smaller.

1. For each approved problem, propose one to three fixes at the level of plot, character arc, point of view, subplot or chapter order. Give each fix its cost (how many chapters it touches) and what it puts at risk.
2. Recommend one fix per problem and check that the recommended fixes do not conflict with each other or with the strengths to protect.
3. Produce a revised chapter map: a table with each chapter's current summary, its fate (keep, cut, merge, move, split, rewrite, new) and the reason. Show the new running order.
4. Check causality across the revised map: each major event should follow from a choice or a consequence, not a coincidence. Flag any link that breaks.
5. Re-check the shape percentages against step 1.
6. Give a work order: which chapters to revise first so later work is not undone.

Write the document with sections Fixes, Revised chapter map, Causality check, Shape after revision, Work order.

Stop and wait for the author to approve the structural plan. Remind them that the scene-level pass starts once they have made, or at least drafted, these structural changes.

Save this step's result to `revision/02-structural-plan.md`.

**Gate:** stop here and wait for the user's approval before step 3 (scenes).

### Step 3: Scene-level pass

Make each scene earn its place in the approved structure.

1. Ask the author which chapters to work on in this session (two to four at a time works best) and to paste them. Stop until they do.
2. For every scene in the pasted chapters, record in a table: the viewpoint character's goal, the conflict, the turn, the value shift from start to end, and whether the scene moves plot, character or both.
3. Flag scenes with no turn, scenes that repeat a beat already delivered elsewhere, scenes that enter too early or leave too late, and point-of-view slips.
4. For each flagged scene, propose a specific fix (cut, merge with another scene, add a reversal, start later, end on the open question) and why.
5. Check pacing: alternation of tension and release, and chapter endings that pull forward.
6. Note continuity issues (names, timeline, objects, injuries) you spot, with chapter references.

Write the document with sections Scene table, Flagged scenes and fixes, Pacing, Continuity.

Stop and wait for the author to approve or adjust the fixes. Offer to repeat this step for the next batch of chapters before moving on to the line pass.

Save this step's result to `revision/03-scene-pass.md`.

**Gate:** stop here and wait for the user's approval before step 4 (lines).

### Step 4: Line-level pass

Teach the author their own sentence-level habits so they can fix the whole book, not just the sample.

1. Ask for one revised chapter (or 2,000 to 4,000 words) that the author considers structurally done, and stop until it is pasted.
2. Identify the author's recurring line-level patterns, with counts and examples: filter words, crutch words, adverb-heavy tags, repeated sentence openings, over-explaining after dialogue, cliché, and runs of same-length sentences.
3. Line-edit one passage of about 300 words as a demonstration: show the original and the edited version side by side, and explain each change in a short note. Preserve the author's voice; do not modernise or flatten deliberate style.
4. Give a self-edit checklist built from this author's actual patterns, ordered by frequency, with a search term for each pattern where one exists (for example search for "began to", "just", "felt").
5. Note any voice inconsistencies between this chapter and earlier pasted chapters.

Write the document with sections Your patterns, Demonstration edit, Self-edit checklist, Voice notes.

Stop and wait for the author to approve before preparing the beta-reader brief.

Save this step's result to `revision/04-line-pass.md`.

**Gate:** stop here and wait for the user's approval before step 5 (beta-brief).

### Step 5: Beta-reader brief

Set up beta readers to test whether the revision worked.

1. Turn the approved fixes from steps 2 to 4 into the questions beta readers can actually answer: reader experience, not craft jargon (for example "Where did you put the book down?" rather than "Is act two saggy?").
2. Write a brief to send beta readers: what the book is, what kind of feedback is wanted and not wanted (no line edits from readers), the deadline, and how to give feedback (chapter-end questions plus a short final questionnaire).
3. Write three to five chapter-end check-in questions placed at the chapters where the revision made the biggest changes, and eight to ten final questions covering the promise of the opening, the protagonist, the midpoint, the ending and the overall pull.
4. Recommend the number and mix of readers (genre readers versus writers) for the author's goals.
5. Give a simple way to tally feedback: one note from one reader is a data point; the same note from three readers is a revision task.

Write the document with sections Brief to readers, Chapter check-ins, Final questionnaire, Reader mix, Reading the feedback.

Save this step's result to `revision/05-beta-reader-brief.md`.
