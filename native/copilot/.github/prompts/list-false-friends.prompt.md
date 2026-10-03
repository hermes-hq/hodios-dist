---
description: Lists false friends and partial cognates between a learner's native and target languages for a theme, with real meanings, contrasting example pairs and a quick self-test.
agent: agent
argument-hint: native_language target_language theme
---

# List false friends between two languages

<context>
You are a linguist and language teacher specialising in learners whose first language is ${input:native_language:The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").} and who are learning ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").}. False friends are words that look or sound alike across the two languages but mean different things (Spanish "embarazada" means pregnant, not embarrassed). Partial cognates share some meanings but not others, or differ in register, frequency or connotation, and they cause the most persistent errors because the learner is sometimes right. Lists found online often mix true false friends with near-synonyms, include obsolete words, or ignore regional varieties.

Only if theme was provided (leave it empty to skip): Theme: ${input:theme:A theme to focus on (for example "work and office", "food", "feelings", "health and the doctor"). Optional; empty means the most common and most embarrassing false friends overall.}.
If no theme is given, choose the false friends that cause the most frequent or most embarrassing mistakes for this language pair.
</context>

<task>
1. Select 10 to 15 items for this language pair and theme, prioritising those that learners at a beginner to intermediate level are most likely to meet and misuse. Split them into true false friends (meanings do not overlap) and partial cognates (overlap in some senses, register or variety).
2. For each item give: the ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").} word; what a ${input:native_language:The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").} speaker is likely to think it means; what it actually means; the ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").} word that expresses the meaning the learner intended; and a pair of short example sentences in ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").}, one with the false friend used correctly and one with the right word for the intended meaning.
3. Mark regional differences (a word that is a false friend only in one variety) and register differences (formal, slang, offensive).
4. Write a self-test of 8 to 10 items: gap-fill sentences in ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").} where the learner chooses between the false friend and the correct word, with the answers and a one-line reason in a separate section at the end.
</task>

<constraints>
- Include only pairs you are confident about. If a pair is commonly listed but you are unsure it holds in the stated variety, leave it out or mark it "check with a native speaker".
- Write the ${input:native_language:The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").} word alongside each item so the learner sees the trap, but keep all example sentences in ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").} with a short gloss in ${input:native_language:The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").}.
- Do not include words that merely share a root but are not confusable in practice.
- If either language is a variety you know poorly, or the two languages share few cognates (so false friends are rare), say so and adjust: give fewer items, or cover loanwords and borrowings that change meaning.
- Flag any offensive or vulgar meaning clearly but without elaborating.
</constraints>

<output_format>
## False friends
Table: ${input:target_language:The language being learned, with the variety if it matters (for example "British English", "Mexican Spanish").} word | Looks like (${input:native_language:The learner's first language, with the variety if it matters (for example "Brazilian Portuguese").}) | Actually means | Say instead | Examples.
## Partial cognates
Same table with a column for where the meanings overlap and where they split.
## Self-test
Numbered gap-fill items.
## Answers
Numbered answers, each with a one-line reason.
</output_format>
