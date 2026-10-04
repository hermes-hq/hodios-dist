---
name: video-production-track
description: Takes a video from idea to hook, script, title and thumbnail, and description, pausing for approval between steps. Use when producing a YouTube video end to end.
license: CC0-1.0
arguments:
  - topic
argument-hint: <topic>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: video
  source: https://hermes-ide.com/prompts/video-production-track
  catalog: 2026.1004.1
---

# Video production track

## Inputs

- `topic` (required): The video idea or subject, with any notes, sources or constraints you already have.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Produces a video about "$topic" one approved step at a time: a sharpened idea with a clear promise to the viewer, then the opening hook, then the full script, then the title and thumbnail package, then the description. Each step produces one artifact and stops for the creator's approval or edits; later steps build on the approved versions and never re-open settled decisions without asking. The promise approved in step 1 is the contract for every later step: the hook sets it up, the script pays it off, and the packaging advertises it honestly. The creator owns every creative decision; the assistant drafts, checks consistency between steps and flags gaps it cannot fill without inventing facts. If the creator asks to skip the approvals, confirm once that later steps will then build on unreviewed choices; if they agree, run the remaining steps in one reply, state the choice made at each skipped gate, and keep every placeholder visible.

## Steps

Work through these steps in order. Do not skip a gate.

1. idea (plan)
2. hook (build)
3. script (build)
4. packaging (build)
5. description (ship)

### Step 1: Idea and promise

Turn "$topic" into a video idea that a specific viewer would click and finish.

1. Ask the creator, in one message, for anything not already given: the channel and its usual audience, the target length, what they personally know or have done that makes them credible on this topic, any footage or examples they can show, and what the video should achieve (views, subscribers, leads, teaching).
2. When you have the answers, write:
   - **Viewer:** who it is for, in one sentence, and what they already know.
   - **Promise:** one sentence: by the end, the viewer will know, be able to do, or have seen what.
   - **Angles:** three distinct angles on the topic (for example a tutorial, a mistake-driven list, a test or experiment, a story), each with a one-line pitch and why it would get clicked. Recommend one.
   - **Proof points:** the examples, demonstrations or facts the video will rest on, marked as either supplied by the creator or still needed.
   - **Risks:** anything that makes the idea hard to deliver (missing footage, unverifiable claims, a crowded topic).

Stop and wait for the creator to approve or edit the angle and promise. Do not write hooks yet.

**Gate:** stop here and wait for the user's approval before step 2 (hook).

### Step 2: Hook

Write the first 15 to 30 seconds for the approved angle of "$topic".

1. Write five hook options, each using a different technique (for example result first, bold claim, the viewer's problem as a question, a mistake and its cost, a story that starts mid-action). For each, give the spoken lines, what is on screen at 0:00, and the open loop it creates.
2. Every option must set up the approved promise and nothing the video will not deliver.
3. No greeting, channel intro or "in this video" before the hook lands.
4. Recommend one and say why in one sentence.

Stop and wait for the creator to choose or edit a hook. Do not write the script yet.

**Gate:** stop here and wait for the user's approval before step 3 (script).

### Step 3: Script

Write the full script for "$topic", starting from the approved hook.

1. Use the approved hook verbatim as the opening, then order the body so value arrives early and escalates. One point per segment, each with a concrete example or demonstration from the approved proof points.
2. Add a pattern interrupt every 45 to 90 seconds (a shot change, B-roll, an on-screen graphic, a question, a quick story) and mark it `[INTERRUPT: …]`. Mark editor cues as `[ON SCREEN: …]` and `[B-ROLL: …]`.
3. Place one soft call to action after a high-value moment and one end call to action pointing to a specific next video or action. Avoid lines that signal the ending before the last 20 seconds.
4. Budget about 150 spoken words per minute of the approved length.
5. Where a fact, number or story is needed but was not supplied, insert a bracketed placeholder instead of inventing it, and list all placeholders at the end with the word count.

Stop and wait for approval or edits. Do not write titles or thumbnails yet.

**Gate:** stop here and wait for the user's approval before step 4 (packaging).

### Step 4: Title and thumbnail

Package the approved script for "$topic" so the right viewers click and are not disappointed.

1. Write six title and thumbnail pairs. The thumbnail shows and the title tells: they work together and do not repeat the same words.
   - Title: under 60 characters, the most important words first.
   - Thumbnail: one focal subject, at most four words of text, high contrast, readable at phone size. Describe the composition, the subject's expression or the key object, and the text.
2. For each pair, name the curiosity mechanism (result, contrast, mystery, stakes, before and after) and check it against the script: the payoff it implies must arrive in the video, ideally in the first minute.
3. Recommend two pairs to test against each other and say what each tests.

Stop and wait for the creator to choose a package. Do not write the description yet.

**Gate:** stop here and wait for the user's approval before step 5 (description).

### Step 5: Description

Write the description for the approved video about "$topic".

1. First two lines: the promise in plain language with the main search phrase used naturally. These lines show before "more", so they must stand alone.
2. A short paragraph on what the video covers and who it is for.
3. Chapters from the approved script's timestamps, starting at `0:00`, at least three, in ascending order, each at least 10 seconds long and named for what the viewer gets. Tell the creator to adjust the times to the final edit.
4. Links the creator supplied, labelled. Never invent a URL; use `[LINK: …]` placeholders for anything mentioned but not supplied.
5. The end call to action from the script, in one line.
6. Finish with a pre-publish checklist: placeholders still open, chapter times to confirm against the edit, and any claim in the packaging that the final cut must still deliver.
