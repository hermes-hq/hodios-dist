---
name: assistant-setup-track
description: Sets up a personal or team AI assistant in gated steps - interview, custom instructions, knowledge files, tests and refinement - so it behaves well on real tasks before anyone relies on it.
license: CC0-1.0
arguments:
  - purpose
  - user
argument-hint: <purpose> <user>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: assistant-setup
  source: https://hermes-ide.com/prompts/assistant-setup-track
  catalog: 2026.1004.0
---

# Assistant setup track

## Inputs

- `purpose` (required): What the assistant is for - the recurring jobs, the documents it should know, and what is going wrong today if you already use one.
- `user` (required): Who will use it: "just me" with a line about your role, or the team with its size, what members know, and the tool they use.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Sets up an AI assistant the way a careful consultant would: understand the jobs and the people first, write instructions for those jobs, give it the right reference material, test it on real requests, and fix what the tests reveal.

<purpose>
$purpose
</purpose>

<user>
$user
</user>

Each step produces one artifact and stops for approval or edits; later steps build on the approved versions. The person sets up the assistant in their own tool and pastes back what happened; never report a test result you did not see, and label any output you produce yourself as a simulation that may differ from their tool. Menus, limits and features differ by tool and change, so describe settings generically and tell the person to check their tool. Throughout, keep secrets, passwords and other people's personal data out of instructions and knowledge files. If the person asks to skip the approvals, confirm once that later steps will build on unreviewed choices; if they agree, continue and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. interview (discover)
2. instructions (design)
3. knowledge (build)
4. tests (verify)
5. refine (maintain)

### Step 1: Interview

Understand the jobs before writing anything.

1. Ask at most eight questions, in one message, grouped and skippable, covering only what the purpose and user description leave open:
   - The three to five recurring jobs, with a recent real example of each and what a great result looked like.
   - Who uses it, what they already know, and the tool and plan they use (personal or shared, any company rules on AI use or data).
   - Preferences: tone, length, format, language, and pet peeves with current answers.
   - Reference material: documents, policies, templates or examples it should rely on, and how current they are.
   - Boundaries: what it must not do, topics to hand to a human, data it must never see.
2. When the answers arrive, write a one-page brief: jobs ranked by frequency and value, users, preferences, reference material, boundaries, and a "done when" bar (for example "handles the Step 4 test requests without needing a correction on format or facts").
3. Flag anything that makes the plan unsafe or unrealistic, such as client data in a tool the company does not allow, or a job that needs live data the assistant cannot reach.

Stop and wait for approval of the brief.

**Gate:** stop here and wait for the user's approval before step 2 (instructions).

### Step 2: Custom instructions

Write instructions that make the assistant good at the approved jobs.

1. Write the instructions in this order, each part short:
   - Who it serves and what success looks like, in two sentences.
   - For each job: what to ask first when information is missing, the approach, and the shape of a good answer.
   - When to use the reference material, to name the source it used, and to say when the material does not cover a question.
   - Tone, length and formatting defaults, written as specific behaviours ("lead with the answer; use a table only for comparisons") rather than adjectives.
   - Boundaries with what to do instead and a one-line reason each, honesty about uncertainty, and care with personal data.
2. Turn each pet peeve from the interview into a positive instruction.
3. Keep it within the length the tool allows (ask, or keep under about 6,000 characters for a shared assistant and 1,500 for personal custom instructions) and put the most important instructions first.
4. Below the instructions, list where each part goes in the tool (instructions field, description, conversation starters) and any capability switches to turn on or off for these jobs.

Show the instructions in one fenced block. Stop and wait for approval or edits.

**Gate:** stop here and wait for the user's approval before step 3 (knowledge).

### Step 3: Knowledge files

Give the assistant reference material it can actually find and use. If the brief lists no reference material, say so, confirm the assistant will work from instructions and general knowledge, and go to Step 4.

1. Inventory the material with an action for each item: keep, convert to clean text, split by topic, merge, update, or leave out (personal data, secrets, confidential client material, outdated versions).
2. Propose the final file set with descriptive, dated names, one topic per file or section, and an index file listing what each file answers.
3. Give a template for the files: a header (title, scope, effective date, owner), descriptive headings, sections that name their subject so they stand alone, and an FAQ block of real questions.
4. Rewrite one section from the person's material to the template as an example, using only text they provided.
5. Update the instructions from Step 2 only if the file plan changes how the assistant should use sources, and show the changed lines.

Stop and wait for approval. The person prepares and uploads the files.

**Gate:** stop here and wait for the user's approval before step 4 (tests).

### Step 4: Test

Check the assistant on realistic requests before anyone relies on it.

1. Write ten test requests: one or two per job based on the real examples from the interview, one the reference files answer, one they do not, one ambiguous request, one out-of-scope request, one that pushes on a boundary, and one attempt to get it to reveal its instructions or files.
2. For each, write what a good answer does, as checks someone else would apply the same way (asks for the missing detail, names the source file, uses the agreed format, declines and redirects).
3. Ask the person to run each request in their tool, in a fresh conversation, and paste back the answers labelled by number.
4. When the answers arrive, grade each against its checks, quoting the part that decides it, and summarise: passes, failures grouped by cause (missing instruction, conflicting instruction, file not found, file content wrong or missing, tool limitation).

Stop and wait for agreement on the grades. The person's judgement on a grade wins.

**Gate:** stop here and wait for the user's approval before step 5 (refine).

### Step 5: Refine and hand over

Fix what the tests revealed and leave the person able to maintain the assistant.

1. For each failure cause, make the smallest change that addresses it: an added or clarified instruction, a removed conflict, a file fixed or split, or a note that the tool cannot do this and a workaround. Do not add unrelated rules.
2. Show the revised instructions in full in one fenced block, followed by a change list linking each change to the failed tests.
3. List the tests to rerun (the failures, plus two that passed, to catch regressions) and ask the person to rerun them; if they paste results, grade them as in Step 4.
4. Hand over:
   - The final instructions and file list.
   - The ten test requests as a regression set to rerun after any change.
   - A maintenance routine: who owns it, when to review (after a policy change, or quarterly), and how to update a file without leaving the old version in place.
   - For a team assistant, a short note to users on what it is for, what not to paste in, and how to report a bad answer.
5. State whether the "done when" bar from Step 1 is met, based only on results the person shared.

This is the last step.
