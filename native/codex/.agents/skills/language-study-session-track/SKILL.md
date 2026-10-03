---
name: language-study-session-track
description: Runs a 45-minute language study session from review warm-up through new input, controlled practice and free production to a recap of words to keep, checking in after each step.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: language-learning
  source: https://hermes-ide.com/prompts/language-study-session-track
  catalog: 2026.1003.0
---

# Language study session track

## Inputs

- [LANGUAGE] (required): The language being studied, with the variety if it matters (for example European Portuguese, Mexican Spanish).
- [LEVEL] (required): The learner's current CEFR level (A1 to C2) or a plain description such as "upper beginner". Sets the level of all input and tasks.
- [TOPIC] (optional): Theme or grammar point for today's session (for example "renting a flat", "the subjunctive after emotions"). Optional; empty means the assistant proposes one.
- [NATIVE_LANGUAGE] (optional; default: English): The learner's first language, used for instructions below A2, for translation items and to explain typical transfer errors. Optional; empty means English.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs one 45-minute study session in [LANGUAGE] at level [LEVEL], step by step: a 5-minute review warm-up, about 10 minutes of new input, 10 minutes of controlled practice, 15 minutes of free production with corrections, and a 5-minute recap. Only if [TOPIC] was provided: Today's topic: [TOPIC]. If no topic is given, the first step proposes two or three that fit the level and the learner picks one.

Each step is one short block of work that ends with a checkpoint: the assistant stops, waits for the learner's answers or "next", and adapts the following step to how this one went. Later steps reuse the words and errors from earlier ones, so the session hangs together. Times are guides; the learner can stretch or skip a step, and the assistant says what the skip costs.

Throughout: keep all input at or slightly above [LEVEL]; give instructions in [LANGUAGE] from A2 upward and in [NATIVE_LANGUAGE] below that, and use [NATIVE_LANGUAGE] for meanings and translation items; never invent the learner's previous material, and ask for it if a review needs it; and say so when unsure about a regional usage instead of teaching a guess as fact.

## Steps

Work through these steps in order. Do not skip a gate.

1. warm-up (verify)
2. input (learn)
3. controlled-practice (learn)
4. free-production (learn)
5. recap (review)

### Step 1: Review warm-up (about 5 minutes)

Wake up what the learner already knows before adding anything new.

1. Ask, in one short message, for the words, phrases or errors from recent sessions they want reviewed (a pasted list, flashcards, last session's recap). If they have none, say you will review high-frequency language for [LEVEL] related to the topic instead. If no topic was given, also offer two or three topics that suit [LEVEL] and ask them to pick.
2. Run a quick retrieval round of 6 to 8 items: mixed recall from [NATIVE_LANGUAGE] into [LANGUAGE], gap-fills and one "say it differently" item. Put the items they are most likely to have forgotten first. Do not show answers yet.
3. When they answer, mark each item right, almost (meaning clear, form wrong) or missed, give the correct form, and note which items to recycle later in the session.

Stop here and wait for the learner to answer the retrieval round, then for "next". Do not present new material in this step.

**Gate:** stop here and wait for the user's approval before step 2 (input).

### Step 2: New input at level (about 10 minutes)

Give the learner something real to understand before asking them to produce anything.

1. Write a short text in [LANGUAGE] on the chosen topic, pitched at [LEVEL]: about 80 to 120 words at A1–A2, 150 to 220 at B1–B2, 250 to 350 at C1–C2. Use a natural form (a message, a dialogue, a short article, a voice-note transcript), not a list of sentences. Work in 6 to 10 new useful items (words, chunks or one grammar pattern) and reuse at least two missed items from the warm-up.
2. Before the text, give one gist question to read for. After it, give 3 or 4 detail questions.
3. Below the questions, list the new items: the item as used in the text, its meaning, and one note (gender, irregular form, register, a typical collocation). Do not explain grammar at length; if the text carries a pattern, show it in a two-line note with the examples from the text.

Stop and wait for the learner's answers to the questions. Check them briefly, clear up anything they misunderstood, then wait for "next".

**Gate:** stop here and wait for the user's approval before step 3 (controlled-practice).

### Step 3: Controlled practice (about 10 minutes)

Make the new items automatic with tasks where the right answer is predictable.

1. Write 8 to 10 short items that each use one new item or the pattern from step 2, moving from easy to harder: recognition (choose the right form), then gap-fill, then transformation (change tense, person or formality), then two short translations from [NATIVE_LANGUAGE] into [LANGUAGE].
2. Number the items and do not show answers.
3. When the learner answers, mark each one. For a wrong answer, give a hint first and let them try once more before you give the correct form and a reason of a few words.
4. Note which items were still shaky; they come back in step 4.

Stop and wait for answers, then for "next". If the learner got fewer than half right, offer a second short round on the weakest item before moving on.

**Gate:** stop here and wait for the user's approval before step 4 (free-production).

### Step 4: Free production with corrections (about 15 minutes)

Let the learner use the language for something of their own.

1. Set one communicative task on the topic that naturally needs today's items, sized to [LEVEL]: answer a message, describe an experience, give and justify an opinion, or role-play a short exchange where you play the other person. State the task in two or three lines and say which items they should try to use.
2. If it is a role-play, stay in role in [LANGUAGE] for 6 to 10 turns, keep your turns short, and do not correct mid-conversation unless a misunderstanding blocks the exchange.
3. When the learner has finished, step out of the task and give feedback:
   - One line on how well the task was achieved.
   - At most five corrections, prioritising errors on today's items, errors that blocked meaning and errors they repeated: their version → correct version · a reason of a few words.
   - Two or three phrases that would have sounded more natural, taken from what they tried to say.
4. Ask them to redo one or two of their own sentences with the corrections.

Stop and wait for the redo, then for "next".

**Gate:** stop here and wait for the user's approval before step 5 (recap).

### Step 5: Recap and words to keep (about 5 minutes)

Close the session so the next one can start from it.

Write the recap:

- **Today:** topic, level and one line on what the learner can now do that they could not at the start.
- **Words to keep:** 6 to 10 items from today, chosen for usefulness rather than difficulty, as a table: [LANGUAGE] item | meaning | example sentence from today. Include items that were shaky in steps 3 and 4.
- **Error to watch:** the one error that came up most, with the correct pattern.
- **Review schedule:** when to review the words to keep (tomorrow, in three days, in a week), and a flashcard-ready block of the same items, one per line as `front ; back`.
- **Next session:** one suggested topic that builds on today.

This is the last step; no checkpoint follows.
