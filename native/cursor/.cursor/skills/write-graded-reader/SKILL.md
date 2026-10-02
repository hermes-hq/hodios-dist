---
name: write-graded-reader
description: Writes a short story at a CEFR level that recycles the words a learner is studying, with a glossary and comprehension questions. Use for reading practice that fits your level.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/write-graded-reader
  catalog: 2026.1002.2
---

# Write a graded reader

## Inputs

- [TARGET_LANGUAGE] (required): Language of the story, with the variety if it matters.
- [LEVEL] (required; one of: A1, A2, B1, B2, C1): Learner's CEFR level; controls length, grammar and vocabulary.
- [INTERESTS] (optional): Topics, genres or settings the learner enjoys. Optional.
- [TARGET_WORDS] (optional): Words or phrases the learner is studying, one per line or comma-separated. Optional.
- [NATIVE_LANGUAGE] (optional; default: English): Language for the glossary meanings.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write graded readers in [TARGET_LANGUAGE]: short, genuinely engaging stories controlled for level. Reading research suggests learners read fluently and pick up new words from context when about 98% of the running words are already known to them, so level control matters more than literary ambition. A story that is too hard becomes decoding; one that is dull does not get finished.

Level (CEFR): [LEVEL]
Only if [INTERESTS] was provided: Learner's interests: [INTERESTS]
Only if [TARGET_WORDS] was provided: Words the learner is studying:
<target_words>
[TARGET_WORDS]
</target_words>
</context>

<task>
1. Write a complete story with a beginning, a turn and an ending, set in something the learner cares about if interests are given.
2. Keep to the level:
   - A1: 150–250 words, present tense, short main clauses, high-frequency words, a lot of repetition.
   - A2: 250–400 words, simple past and future forms, common connectors.
   - B1: 400–600 words, the full range of everyday tenses, some subordinate clauses, a little dialogue.
   - B2: 600–900 words, varied structures and some idiomatic language.
   - C1: 900–1,200 words, natural prose with nuance, implicit meaning and register shifts.
   For languages written without spaces, such as Chinese or Japanese, count about two characters as one word.
3. If target words are given, use every one at least twice, in contexts that make the meaning guessable. Bold each the first time it appears. If one cannot fit naturally, leave it out and say so instead of forcing it.
4. Build a glossary of the target words plus any word likely to be above [LEVEL], glossed in [NATIVE_LANGUAGE] with the meaning used in this story.
5. Write 6 comprehension questions in [TARGET_LANGUAGE], worded at the level: two literal, two inference, two about a word or phrase in context. Put the answers after the questions.
</task>

<constraints>
- No more than about 2% of the words should be above the level, not counting target words. Prefer rewriting a sentence to glossing it.
- Natural [TARGET_LANGUAGE], the kind of text a native writer would produce for this level, not a translation of an English story.
- No real people. Keep content suitable for adult learners in general; avoid gratuitous violence.
- Use a consistent regional variety and say which one if it matters.
</constraints>

<output_format>
## Story
A title, then the story.
## Glossary
Table: Word | Meaning in this story.
## Questions
Numbered 1–6.
## Answers
Numbered 1–6, short.
## Target words used
Each target word with how many times it appears, or "None given".
</output_format>
