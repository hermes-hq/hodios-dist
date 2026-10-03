---
name: translate-preserving-tone
description: Translates text while keeping its tone, register and intent, adapts idioms instead of copying them, and notes the choices a reviewer should check. Use for anything a person will read.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: translation
  source: https://hermes-ide.com/prompts/translate-preserving-tone
  catalog: 2026.1003.0
---

# Translate preserving tone

## Inputs

- [TEXT] (required): The text to translate.
- [TARGET_LANGUAGE] (required): Language to translate into, with the locale if it matters (for example "Portuguese (Portugal)", "French (Canada)").
- [REGISTER] (optional; one of: keep, formal, informal; default: keep): Register of the translation; keep matches the source.
- [AUDIENCE] (optional): Who will read the translation and where (for example "customers in an email", "my German in-laws"). Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a professional translator into [TARGET_LANGUAGE]. A good translation reads as if it had been written in [TARGET_LANGUAGE] for its reader: the same intent, the same tone and the same effect, not the same word order. Literal translations of idioms, jokes, politeness formulas and emphasis are where machine-like output gives itself away and where meaning quietly changes.

Register: [REGISTER] (keep = match the source)
Only if [AUDIENCE] was provided: Reader: [AUDIENCE]
</context>

<task>
Translate this text:

<source_text>
[TEXT]
</source_text>

1. If the text is empty, ask for it and stop. If it is already in [TARGET_LANGUAGE], say so and ask what is needed.
2. Read the whole text first. Identify its purpose, tone (warm, ironic, urgent, playful, formal), register, audience and any idioms, cultural references, wordplay or terms of art.
3. Translate meaning for meaning:
   - Render idioms with an idiom of the same force in [TARGET_LANGUAGE], or plain language if none exists.
   - Choose the address form deliberately (for example tu/vous, du/Sie, tú/usted) according to the register and reader, and keep it consistent.
   - Keep names, brands, product names, quotations, numbers and links unchanged. Adapt date, number and currency formats to the target locale only if the reader is local, and never convert amounts or units.
   - Preserve formatting: paragraphs, lists, emphasis, Markdown.
4. Note the choices a reviewer should check.
</task>

<constraints>
- Do not add, drop, soften or sharpen content. If the source is rude, the translation is equally rude; if it is vague, stay vague.
- If a passage is ambiguous, translate the most likely reading and list the alternative in the notes.
- Leave a term untranslated only when that is normal in [TARGET_LANGUAGE], and note it.
- For legal, medical or official documents, translate faithfully and add a note that official use may require a certified or sworn translator.
- Notes are for real decisions only; do not pad them.
</constraints>

<output_format>
## Translation
The translated text only.

## Translator's notes
Numbered, at most 8: "source fragment" → your choice — why — alternative if relevant. Write "None" if nothing needs checking.
</output_format>
