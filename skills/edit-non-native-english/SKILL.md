---
name: edit-non-native-english
description: Polishes English written by a non-native professional into natural, idiomatic text in the right register, and lists their recurring error patterns with one-line rules so they improve over time.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: editing
  source: https://hermes-ide.com/prompts/edit-non-native-english
  catalog: 2026.1004.1
---

# Polish English written by a non-native speaker

## Inputs

- [TEXT] (required): Your text in English, such as an email, report section, abstract, cover letter or post.
- [WRITER_FIRST_LANGUAGE] (optional): Your first language, for example Portuguese, German or Mandarin. It helps explain why certain patterns happen; leave empty if you prefer.
- [REGISTER] (optional; one of: business, academic, casual; default: business): How formal the text should be. Business for work emails and documents, academic for papers and theses, casual for chat and social posts.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Professionals who write in English as a second language usually know exactly what they mean; the problems are articles, prepositions, verb tenses, word order, false friends, collocations ("make a research" instead of "do research"), and register that is too formal or too blunt for English readers. A plain proofread fixes the text but teaches nothing, so the same errors come back next week. The writer needs the text fixed, the few changes that affect meaning or impression called out, and their own recurring patterns explained with simple rules they can apply themselves. Over-editing is a real risk: rewriting everything into a native-speaker style the writer could never reproduce, or "correcting" valid international English, makes them feel their English is worse than it is.
</context>

<task>
Polish this text to natural [REGISTER] English.Only if [WRITER_FIRST_LANGUAGE] was provided:  The writer's first language is [WRITER_FIRST_LANGUAGE].

<text>
[TEXT]
</text>

1. If the text is empty, ask for it and stop.
2. Fix errors in grammar, articles, prepositions, tense and aspect, word order, collocations, false friends and punctuation. Replace phrases that are grammatical but unnatural with what an English-speaking professional would write.
3. Adjust register to [REGISTER]: for business, direct and polite, with softened requests ("Could you…" rather than "You must…") and no archaic formality ("Kindly do the needful", "Herewith"); for academic, precise and hedged appropriately; for casual, relaxed but clear.
4. Keep the writer's meaning, structure, content and level of detail. Keep their voice: do not replace simple correct words with fancier ones, and do not change correct sentences just to sound more native.
5. Call out the changes that matter most: anything that changed or could have changed the meaning, and anything that could make the writer sound rude, too informal or unsure. Put these first.
6. Identify the writer's three to five recurring patterns (errors that appear more than once, or a type of error), each with an example from their text, the correction, and a one-line rule they can remember. If the first language is given and the pattern is a well-known transfer from it, mention that briefly and only when you are confident.
7. Quote one to three phrases from their text that already work well, so they keep using them. Choose only genuinely good ones; for a very short or heavily corrected text, write "None this time" rather than praising something weak.
</task>

<constraints>
- Do not add content, claims or politeness formulas the writer did not intend.
- Keep technical terms, names, numbers and quoted material unchanged.
- Use the spelling variety the text mostly uses (US or UK); if mixed, choose the dominant one and say so.
- Explanations in simple English, short sentences, no linguistic jargon beyond common terms like "article" or "preposition".
- Be encouraging and factual; do not comment on the writer's English level.
</constraints>

<output_format>
## Polished text
The full polished text.
## Changes that matter
Up to five bullets: original → polished, and why it matters (meaning or impression).
## Your patterns
Table: Pattern · Example from your text · Correction · Rule to remember.
## Phrases to keep
One to three bullets quoting what already works well, or "None this time".
</output_format>
