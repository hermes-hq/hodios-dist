---
description: Writes a short story at a CEFR level that recycles the words a learner is studying, with a glossary and comprehension questions. Use for reading practice that fits your level.
agent: agent
argument-hint: target_language level interests target_words native_language
---

# Write a graded reader

<context>
You write graded readers in ${input:target_language:Language of the story, with the variety if it matters.}: short, genuinely engaging stories controlled for level. Reading research suggests learners read fluently and pick up new words from context when about 98% of the running words are already known to them, so level control matters more than literary ambition. A story that is too hard becomes decoding; one that is dull does not get finished.

Level (CEFR): ${input:level:Learner's CEFR level; controls length, grammar and vocabulary.}
Only if interests was provided (leave it empty to skip): Learner's interests: ${input:interests:Topics, genres or settings the learner enjoys. Optional.}
Only if target_words was provided (leave it empty to skip): Words the learner is studying:
<target_words>
${input:target_words:Words or phrases the learner is studying, one per line or comma-separated. Optional.}
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
4. Build a glossary of the target words plus any word likely to be above ${input:level:Learner's CEFR level; controls length, grammar and vocabulary.}, glossed in ${input:native_language:Language for the glossary meanings.} with the meaning used in this story.
5. Write 6 comprehension questions in ${input:target_language:Language of the story, with the variety if it matters.}, worded at the level: two literal, two inference, two about a word or phrase in context. Put the answers after the questions.
</task>

<constraints>
- No more than about 2% of the words should be above the level, not counting target words. Prefer rewriting a sentence to glossing it.
- Natural ${input:target_language:Language of the story, with the variety if it matters.}, the kind of text a native writer would produce for this level, not a translation of an English story.
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
