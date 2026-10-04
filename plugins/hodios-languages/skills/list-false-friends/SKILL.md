---
name: list-false-friends
description: Lists false friends and partial cognates between a learner's native and target languages for a theme, with real meanings, contrasting example pairs and a quick self-test.
license: CC0-1.0
arguments:
  - native_language
  - target_language
  - theme
argument-hint: <native_language> <target_language> [theme]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/list-false-friends
  catalog: 2026.1004.0
---

# List false friends between two languages

## Inputs

- `native_language` (required): The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").
- `target_language` (required): The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").
- `theme` (optional): A theme to focus on (for example "work and office", "food", "feelings", "health and the doctor"). Optional; empty means the most common and most embarrassing false friends overall.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a linguist and language teacher specialising in learners whose first language is $native_language and who are learning $target_language. False friends are words that look or sound alike across the two languages but mean different things (Spanish "embarazada" means pregnant, not embarrassed). Partial cognates share some meanings but not others, or differ in register, frequency or connotation, and they cause the most persistent errors because the learner is sometimes right. Lists found online often mix true false friends with near-synonyms, include obsolete words, or ignore regional varieties.

Only if theme was provided: Theme: $theme.
If no theme is given, choose the false friends that cause the most frequent or most embarrassing mistakes for this language pair.
</context>

<task>
1. Select 10 to 15 items for this language pair and theme, prioritising those that learners at a beginner to intermediate level are most likely to meet and misuse. Split them into true false friends (meanings do not overlap) and partial cognates (overlap in some senses, register or variety).
2. For each item give: the $target_language word; what a $native_language speaker is likely to think it means; what it actually means; the $target_language word that expresses the meaning the learner intended; and a pair of short example sentences in $target_language, one with the false friend used correctly and one with the right word for the intended meaning.
3. Mark regional differences (a word that is a false friend only in one variety) and register differences (formal, slang, offensive).
4. Write a self-test of 8 to 10 items: gap-fill sentences in $target_language where the learner chooses between the false friend and the correct word, with the answers and a one-line reason in a separate section at the end.
</task>

<constraints>
- Include only pairs you are confident about. If a pair is commonly listed but you are unsure it holds in the stated variety, leave it out or mark it "check with a native speaker".
- Write the $native_language word alongside each item so the learner sees the trap, but keep all example sentences in $target_language with a short gloss in $native_language.
- Do not include words that merely share a root but are not confusable in practice.
- If either language is a variety you know poorly, or the two languages share few cognates (so false friends are rare), say so and adjust: give fewer items, or cover loanwords and borrowings that change meaning.
- Flag any offensive or vulgar meaning clearly but without elaborating.
</constraints>

<output_format>
## False friends
Table: $target_language word | Looks like ($native_language) | Actually means | Say instead | Examples.
## Partial cognates
Same table with a column for where the meanings overlap and where they split.
## Self-test
Numbered gap-fill items.
## Answers
Numbered answers, each with a one-line reason.
</output_format>
