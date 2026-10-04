---
name: plan-vocabulary-instruction
description: Plans explicit vocabulary instruction for a unit, selecting tier 2 and tier 3 words with student-friendly definitions, examples, practice routines across days and a quick check.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/plan-vocabulary-instruction
  catalog: 2026.1004.2
---

# Plan vocabulary instruction for a unit

## Inputs

- [UNIT_TEXT_OR_TOPIC] (required): The unit topic, or better, the text students will read (pasted), so words are chosen from what they will actually meet.
- [GRADE_LEVEL] (required): Grade, age or course, e.g. "Grade 4", "Year 8 history", "adult ESL intermediate".
- [WORD_COUNT] (optional; default: 10): How many words to teach explicitly across the unit.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Students learn most words from reading, but the words that unlock academic texts need explicit teaching. Useful selection follows a tiered view: tier 1 everyday words rarely need teaching; tier 2 words (analyse, reluctant, consequence, significant) appear across subjects and are the best investment; tier 3 words (photosynthesis, feudalism) are subject-specific and are taught with the content. Dictionary definitions rarely help ("ubiquitous: present everywhere"); student-friendly definitions explain the word in everyday language with "describes someone who…" or "if something is…, it…". Words stick through multiple, varied encounters over days: examples and non-examples, using the word in speech and writing, word parts, and connections between words.
</context>

<task>
Plan vocabulary teaching for **[GRADE_LEVEL]**, teaching [WORD_COUNT] words explicitly.

<unit_text_or_topic>
[UNIT_TEXT_OR_TOPIC]
</unit_text_or_topic>

1. **Select words.** From the text (or, if only a topic is given, from texts typical for that topic and level), choose [WORD_COUNT] words: mostly tier 2, plus the tier 3 words essential to the content. For each, say why it earns explicit teaching: it is needed to understand the unit, useful across subjects, or unlikely to be learned from context. If a text was given, only choose words that appear in it.
2. **Teaching card for each word:** a student-friendly definition, an example sentence from the unit context, an example from students' everyday lives, a non-example, word parts or related forms if useful (for example "-ology", "reluctant / reluctance"), and for multilingual learners a cognate note where a common one exists.
3. **Introducing a word:** a short routine (about 2 minutes per word) the teacher repeats: say it, students say it, definition, examples, a quick "yes or no, why?" question, students use it.
4. **Practice across the unit:** a day-by-day plan of short practice activities (5 to 10 minutes) that bring every word back several times, mixing speaking and writing, such as "which word goes with…", example or non-example sorts, word-relationship maps, and challenges to use target words in discussion or writing.
5. **Quick check:** 5 to 8 items that test meaning in context rather than definition recall, with an answer key.
6. **Words to treat lightly:** other unfamiliar words in the text to explain in passing, not teach.
</task>

<constraints>
- Definitions use words simpler than the word being defined and fit the meaning used in this unit; note when a word has a different everyday meaning (for example "table" in science, "power" in maths).
- Do not pick words only because they are long or rare. Prefer words students will meet again.
- If a pasted text has fewer than [WORD_COUNT] words worth teaching, choose fewer and say so.
- Example sentences must be correct, natural and inclusive.
- Keep cognate notes accurate; skip them when you are not sure, and flag false friends only if you are certain.
</constraints>

<output_format>
## Word selection
Table: Word | Tier | Why teach it.
## Teaching cards
One block per word: definition · unit example · everyday example · non-example · word parts · cognate note (if any).
## Introducing a word
The routine as numbered steps with teacher prompts in quotes.
## Practice across the unit
Table: Day | Activity | Words | Time.
## Quick check
Numbered items, then the answer key.
## Words to treat lightly
Word: quick in-passing explanation.
</output_format>
