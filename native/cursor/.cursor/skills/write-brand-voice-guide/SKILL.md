---
name: write-brand-voice-guide
description: Writes a voice and tone guide with voice attributes, tone shifts by situation, vocabulary, mechanics, dos and don'ts, and before-and-after rewrites. Use when defining how a brand writes.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: branding
  source: https://hermes-ide.com/prompts/write-brand-voice-guide
  catalog: 2026.1002.1
---

# Write a brand voice and tone guide

## Inputs

- [BRAND] (required): Who the brand is, what it offers, its audience, its values and how it wants to be perceived. Mention competitors whose voice you want to differ from.
- [SAMPLES] (optional): Existing copy (website, emails, app text, social posts), labelled as good examples or ones to avoid. Optional; with samples, the guide is derived from real writing.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Most voice guides list adjectives every brand claims ("friendly, innovative, human") and give writers nothing to act on. A usable guide makes choices that exclude something ("confident, not cocky"), shows how the voice stays constant while the tone shifts with the situation (a celebration versus a failed payment), and teaches through rewrites a writer can copy.
</context>

<task>
Write a voice and tone guide for this brand.

<brand>
[BRAND]
</brand>
Only if [SAMPLES] was provided: 
<samples>
[SAMPLES]
</samples>

1. If samples were given, analyse them first: what the strongest samples do (sentence length, person, formality, humour, jargon) and where samples are inconsistent. Base the guide on the samples marked good, and cite them.
2. **Voice summary:** 2 to 3 sentences on who the brand sounds like, written in that voice.
3. **Voice attributes:** 3 or 4 attributes, each written as "X, not Y" with a one-line definition, a "this means" and a "this does not mean" list, and a short example. Place the voice on four dimensions (funny to serious, formal to casual, respectful to irreverent, enthusiastic to matter-of-fact) and say where it sits on each.
4. **Tone by situation:** a table covering at least onboarding or welcome, marketing and launch, product instructions, errors and failures, billing and money, apologies or outages, and sensitive moments (bereavement, security incidents, cancellations). For each: the reader's likely state of mind, how the tone shifts, and an example line.
5. **Vocabulary:** words and phrases we use, words we avoid (with the replacement), how to name the product and its features, and jargon rules.
6. **Mechanics:** person (we or you), contractions, sentence and title case, punctuation choices (serial comma, exclamation marks), emoji, numbers and dates, and inclusive language basics.
7. **Before and after:** 5 to 8 rewrites across different situations, each with a one-line reason tied to an attribute. Use real samples where given.
8. **Checklist:** 6 to 8 yes-or-no questions a writer can run before publishing.
</task>

<constraints>
- Every attribute must rule something out. Drop any attribute that could describe any brand.
- Do not make up brand facts, products or claims. If the brand description is too thin to choose attributes (no audience, no values), ask up to three questions and stop.
- Write the guide itself in the voice it describes, except for the tables, which stay plain.
- Humour never appears in errors, money problems or sensitive situations.
</constraints>

<output_format>
Markdown with the contract's sections as `##` headings, in order. Tables for tone by situation and vocabulary. Before-and-after pairs as "Before:" and "After:" lines with the reason below.
</output_format>
