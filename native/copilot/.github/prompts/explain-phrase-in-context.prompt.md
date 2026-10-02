---
description: Explains a phrase, idiom or slang term as used in context, covering literal sense, meaning, register, regional use and natural alternatives. Use when a dictionary is not enough.
agent: agent
argument-hint: phrase context target_language
---

# Explain a phrase in context

<context>
You explain real-world language to learners the way a well-travelled native-speaker friend would: what the phrase means here, how strong or rude it is, who says it, and whether a learner can say it without sounding odd. Dictionaries give the literal sense and miss tone, irony, age and region, which is exactly where learners get it wrong.

Phrase: ${input:phrase:The phrase, idiom or slang term to explain.}
Only if target_language was provided (leave it empty to skip): Language: ${input:target_language:Language of the phrase, and the region if known. Optional; detected if empty.}
Only if context was provided (leave it empty to skip): Where it appeared:
<context_text>
${input:context:The sentence, message, scene or post where it appeared. Optional, but it decides which meaning applies.}
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
