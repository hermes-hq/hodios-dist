---
description: Takes a story from premise to characters, an outline, a sample scene and revision notes, stopping for the author's approval between steps. Use when starting a new novel or story.
agent: agent
argument-hint: working_title seed
---

# Story development track

Develops "${input:working_title:Working title or a short name for the project.}"Only if seed was provided (leave it empty to skip):  (seed: ${input:seed:The idea so far, in any form (a situation, a character, an image, a question). Optional; step 1 asks for it if missing.}) the way a good editor works with an author before the first draft: sharpen the premise, build characters the plot can pressure, outline with causality, test the voice and the outline in one sample scene, then plan the revision. Each step produces one document and stops for approval; later steps build on the approved documents instead of re-asking.

Rules for every step: the author owns the story, so offer options and ask for decisions on anything that defines it (genre, ending, point of view, theme) instead of choosing silently; never contradict an approved earlier step without flagging it; keep each document short enough to read in five minutes; and do not draft beyond the single sample scene in step 4. If the author wants to go faster or skip to drafting, explain in one line what each remaining step protects, offer the fast route (shorter documents, one question per step, a sample scene as soon as the outline is approved), and keep every approval gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. premise (discover)
2. characters (design)
3. outline (plan)
4. scene (build)
5. revise (review)

### Step 1: Premise

Turn the seed of "${input:working_title:Working title or a short name for the project.}" into a premise strong enough to outline.

1. Ask, in one message, only what you cannot infer: the seed idea if none was given, genre and readership, target length (short story, novella, novel), what drew the author to this idea, and anything that must stay (a character, an image, an ending).
2. Once answered, write three distinct premise options. Each has: a logline (protagonist, inciting incident, goal, opposition, stakes); the central dramatic question the ending answers; the thematic question underneath it; and what makes it fresh in its genre.
3. For each option, name the biggest risk (thin opposition, passive protagonist, familiar setup) in one line.
4. Recommend one option and say why, or a merge of two.

Write the document with sections Answers, Options, Recommendation.

Stop and wait for the author to choose or adjust the premise.

Save this step's result to `story-notes/01-premise.md`.

**Gate:** stop here and wait for the user's approval before step 2 (characters).

### Step 2: Characters

Build the cast the approved premise needs.

1. Protagonist: want (external, concrete), need (internal), flaw and the false belief behind it, the wound that taught it, a contradiction, voice notes with two sample lines, and the arc type (positive, negative, flat).
2. Opposition: the antagonist or antagonistic force, with a want that is reasonable from their side and a direct collision with the protagonist's want.
3. Two or three supporting characters, each with a job in the story (mirror, mentor, temptation, cost) and their own small want.
4. A relationship map: one line per important pair saying what each wants from the other and where it will break.
5. Flag any character who has no job in the plot or theme.

Write the document with sections Protagonist, Opposition, Supporting cast, Relationships, Flags. Use names that fit the setting; avoid stock names.

Stop and wait for approval.

Save this step's result to `story-notes/02-characters.md`.

**Gate:** stop here and wait for the user's approval before step 3 (outline).

### Step 3: Outline

Outline the story from the approved premise and characters.

1. Propose the structure that fits (three-act, Save the Cat beats, hero's journey stages, kishotenketsu, or a mystery's clue-and-reveal structure) and say why in one line. Use the author's choice if they have one.
2. Outline the main plot as beats, scaled to the target length, with an approximate position for each. Every link to the next beat is "therefore" or "but"; mark any "and then".
3. Weave in the subplots from the relationship map, noting where each collides with the main plot.
4. Mark where the protagonist's arc beats fall: first challenge to the false belief, the low point, the final choice.
5. Run a causality check and list every coincidence that helps the protagonist, every turning point they do not cause, and every subplot that never touches the main plot, each with a fix.
6. Propose two or three candidate scenes for the sample in step 4: pivotal moments that test the voice and the central conflict.

Write the document with sections Structure, Beat outline (table), Subplots, Arc beats, Causality check, Candidate scenes.

Stop and wait for approval and the choice of sample scene.

Save this step's result to `story-notes/03-outline.md`.

**Gate:** stop here and wait for the user's approval before step 4 (scene).

### Step 4: Sample scene

Write the chosen scene as a test of voice and outline, not as the final draft.

1. Confirm point of view and tense; ask once if the author has not decided.
2. Write a scene card first: the point-of-view character's goal in the scene, the opposition, the turn (how the situation changes), and the value shift (for example trust to betrayal).
3. Write the scene in 800 to 1,500 words. Enter late, leave early, ground it in specific sensory detail, and let the dialogue carry subtext.
4. Avoid stock phrasing ("a testament to", "the air was thick with", "a breath she didn't know she was holding").

Write the document with sections Scene card and Scene.

Stop and wait for the author's reaction. Ask what felt right and what did not.

Save this step's result to `story-notes/04-sample-scene.md`.

**Gate:** stop here and wait for the user's approval before step 5 (revise).

### Step 5: Revision notes

Use the sample scene and the author's reaction to improve the plan before drafting begins.

1. Note what the scene revealed: did the voice work, did the characters behave as designed, did the scene's turn match the outline, and what surprised you or the author.
2. List changes to the earlier documents this implies (premise, characters, outline), each with the reason. Keep it to the changes that matter.
3. Give prioritised notes on the scene itself (at most five), without rewriting it.
4. End with a drafting plan: where to start, the first five scenes to write, and three questions for the author to keep in mind while drafting.

Write the document with sections What the scene showed, Changes to the plan, Scene notes, Drafting plan.

Save this step's result to `story-notes/05-revision-notes.md`.
