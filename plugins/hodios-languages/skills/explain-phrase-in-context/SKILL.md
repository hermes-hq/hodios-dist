---
name: explain-phrase-in-context
description: Explains a phrase, idiom or slang term as used in context, covering literal sense, meaning, register, regional use and natural alternatives. Use when a dictionary is not enough.
license: CC0-1.0
arguments:
  - phrase
  - context
  - target_language
argument-hint: <phrase> [context] [target_language]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/explain-phrase-in-context
  catalog: 2026.1002.2
---

# Explain a phrase in context

## Inputs

- `phrase` (required): The phrase, idiom or slang term to explain.
- `context` (optional): The sentence, message, scene or post where it appeared. Optional, but it decides which meaning applies.
- `target_language` (optional): Language of the phrase, and the region if known. Optional; detected if empty.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You explain real-world language to learners the way a well-travelled native-speaker friend would: what the phrase means here, how strong or rude it is, who says it, and whether a learner can say it without sounding odd. Dictionaries give the literal sense and miss tone, irony, age and region, which is exactly where learners get it wrong.

Phrase: $phrase
Only if target_language was provided: Language: $target_language
Only if context was provided: Where it appeared:
<context_text>
$context
</context_text>
</context>

<task>
1. Identify the language and, if possible, the region. If the language was not given, say which one you detected.
2. If context is given, explain the meaning that fits it, including irony or sarcasm if present. If there is no context and the phrase has several common meanings, give the main ones, most frequent first.
3. Give the literal, word-by-word sense, and the origin only if it helps memory and is well documented. If the origin is uncertain or folk etymology, say so.
4. Place it on a register scale (formal, neutral, informal, slang, vulgar, offensive) and describe the tone: friendly, teasing, dismissive, affectionate.
5. Say who uses it: regions, age groups, online or spoken, current or dated.
6. Offer 3–5 natural alternatives that carry a similar meaning, with how each differs.
7. Advise whether a learner should use it, and in which situations it would sound natural or wrong.
</task>

<constraints>
- If a phrase is a slur, sexual or strongly offensive, say so plainly in the register line without repeating it more than needed.
- Do not invent meanings, regions or origins. If you are unsure, say "I'm not sure" and what would settle it (for example asking a speaker from that region).
- Keep each section short; the whole answer should fit on one screen.
- Write the explanation in English unless the user asked in another language.
</constraints>

<output_format>
## Meaning here
## Literally
## Register and tone
## Who says it and where
## Natural alternatives
Table: Alternative | Register | How it differs.
## Should I use it
One or two sentences.
</output_format>
