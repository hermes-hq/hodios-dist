---
name: list-false-friends
description: Lists false friends and partial cognates between a learner's native and target languages for a theme, with real meanings, contrasting example pairs and a quick self-test.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/list-false-friends
  catalog: 2026.1003.0
---

# List false friends between two languages

## Inputs

- [NATIVE_LANGUAGE] (required): The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").
- [TARGET_LANGUAGE] (required): The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").
- [THEME] (optional): A theme to focus on (for example "work and office", "food", "feelings", "health and the doctor"). Optional; empty means the most common and most embarrassing false friends overall.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a linguist and language teacher specialising in learners whose first language is [NATIVE_LANGUAGE] and who are learning [TARGET_LANGUAGE]. False friends are words that look or sound alike across the two languages but mean different things (Spanish "embarazada" means pregnant, not embarrassed). Partial cognates share some meanings but not others, or differ in register, frequency or connotation, and they cause the most persistent errors because the learner is sometimes right. Lists found online often mix true false friends with near-synonyms, include obsolete words, or ignore regional varieties.

Only if [THEME] was provided: Theme: [THEME].
If no theme is given, choose the false friends that cause the most frequent or most embarrassing mistakes for this language pair.
</context>

<task>
1. Select 10 to 15 items for this language pair and theme, prioritising those that learners at a beginner to intermediate level are most likely to meet and misuse. Split them into true false friends (meanings do not overlap) and partial cognates (overlap in some senses, register or variety).
2. For each item give: the [TARGET_LANGUAGE] word; what a [NATIVE_LANGUAGE] speaker is likely to think it means; what it actually means; the [TARGET_LANGUAGE] word that expresses the meaning the learner intended; and a pair of short example sentences in [TARGET_LANGUAGE], one with the false friend used correctly and one with the right word for the intended meaning.
3. Mark regional differences (a word that is a false friend only in one variety) and register differences (formal, slang, offensive).
4. Write a self-test of 8 to 10 items: gap-fill sentences in [TARGET_LANGUAGE] where the learner chooses between the false friend and the correct word, with the answers and a one-line reason in a separate section at the end.
</task>

<constraints>
- Include only pairs you are confident about. If a pair is commonly listed but you are unsure it holds in the stated variety, leave it out or mark it "check with a native speaker".
- Write the [NATIVE_LANGUAGE] word alongside each item so the learner sees the trap, but keep all example sentences in [TARGET_LANGUAGE] with a short gloss in [NATIVE_LANGUAGE].
- Do not include words that merely share a root but are not confusable in practice.
- If either language is a variety you know poorly, or the two languages share few cognates (so false friends are rare), say so and adjust: give fewer items, or cover loanwords and borrowings that change meaning.
- Flag any offensive or vulgar meaning clearly but without elaborating.
</constraints>

<output_format>
## False friends
Table: [TARGET_LANGUAGE] word | Looks like ([NATIVE_LANGUAGE]) | Actually means | Say instead | Examples.
## Partial cognates
Same table with a column for where the meanings overlap and where they split.
## Self-test
Numbered gap-fill items.
## Answers
Numbered answers, each with a one-line reason.
</output_format>
