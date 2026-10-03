---
name: build-subject-glossary
description: Builds a glossary of a subject's key terms with plain definitions, examples, word roots and commonly confused pairs, plus a flashcard export ready to import.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: studying
  source: https://hermes-ide.com/prompts/build-subject-glossary
  catalog: 2026.1003.2
---

# Build a subject glossary

## Inputs

- [SUBJECT] (required): The subject and topic, for example "A-level Biology, cell structure" or "Intro Macroeconomics".
- [TERMS_OR_MATERIAL] (required): Either a list of terms or a passage of course material (notes, a chapter, slides) to extract the key terms from.
- [LEVEL] (optional): Optional level, for example "Year 9", "first-year university". Sets how technical the definitions are.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Subject vocabulary is where many marks quietly go: students know roughly what "osmosis" or "elasticity" means but cannot define it precisely, mix it up with a near neighbour, or use an everyday meaning where the subject uses a technical one ("significant", "theory", "work"). A good glossary defines each term without using the term itself, anchors it with an example, shows the word parts when they genuinely help recall, and separates the pairs students confuse.
</context>

<task>
Build a glossary for [SUBJECT]Only if [LEVEL] was provided:  at [LEVEL] level.

<terms_or_material>
[TERMS_OR_MATERIAL]
</terms_or_material>

1. If this is a term list, use it. If it is course material, extract the 10 to 30 terms a student would be expected to define or use precisely, and only terms that appear in the material.
2. Group the terms by subtopic, in the order a learner would meet them.
3. For each term write:
   - A plain definition in one sentence that does not use the term or a form of it, accurate at the stated level. If the material defines the term, follow its definition.
   - A concrete example or use in a sentence.
   - Word roots (Greek, Latin or other) only when they help recall and you are sure of them, for example "photo- (light) + synthesis (putting together)". Leave the cell empty otherwise.
   - The term it is most often confused with, if any.
   - A note when the everyday meaning differs from the subject meaning.
4. Collect the commonly confused pairs and explain each difference in one or two lines with a quick test to tell them apart.
5. Produce a flashcard export: one line per term, "term;definition", with no header, ready for import into Anki or Quizlet with semicolon as the separator.
</task>

<constraints>
- Never invent an etymology. A wrong root is worse than none.
- Do not add terms that are not in the list or material, except to name a confused partner.
- Keep definitions short: at most 25 words each.
- If the list is empty or the material contains no subject terms, say so and ask for the terms or a passage.
</constraints>

<output_format>
## Glossary
One table per subtopic: Term | Definition | Example | Roots | Don't confuse with.
Everyday-meaning notes in italics below the relevant table.
## Commonly confused
Bullets: "A vs B": the difference, then the quick test.
## Flashcards
A code block of "term;definition" lines.
</output_format>
