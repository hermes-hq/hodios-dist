---
name: build-localization-glossary
description: Builds a product term base from UI strings, with definitions, do-not-translate terms and proposed translations per locale, so localization stays consistent. Use before the first translation round.
license: CC0-1.0
arguments:
  - source_strings
  - locales
  - product_context
argument-hint: <source_strings> <locales> [product_context]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: localization
  source: https://hermes-ide.com/prompts/build-localization-glossary
  catalog: 2026.1002.1
---

# Build a localization glossary

## Inputs

- `source_strings` (required): The UI strings or catalog to mine for terms, in the source language.
- `locales` (required): Target locales to propose translations for, for example "de-DE, fr-FR, ja-JP".
- `product_context` (optional): What the product does, who uses it, brand names, and any platform it must feel native on (Windows, macOS, iOS, Android).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Without a glossary, each translator and each release picks its own word for the product's core concepts, so "Workspace" becomes three different words in German across one screen, and "Archive" and "Delete" blur together in a language where the first guess was a synonym. A good term base is short, covers the terms that carry product meaning or appear everywhere, defines each one so translators understand the concept rather than the English word, and settles brand names once.
</context>

<task>
Build a localization glossary from these strings:

$source_strings

Target locales: $locales
Product context: $product_context

1. Extract candidate terms:
   - product objects and features ("Workspace", "Board", "Snapshot");
   - recurring UI actions whose differences matter ("Archive" versus "Delete" versus "Remove", "Sign in" versus "Log in");
   - domain terms that users must understand precisely;
   - brand, product and plan names, and code-like tokens.
   Skip generic words that any translator handles consistently.
2. Check the source for its own inconsistencies first: the same concept named two ways, or one word used for two concepts. Report them, because they must be fixed in the source or the glossary will encode the confusion.
3. For each term, record its part of speech, a one-sentence definition of the concept in this product, a real usage example taken from the strings, and whether it is do-not-translate.
4. Propose a translation per locale:
   - For standard concepts (Settings, Preferences, Sign in, Share), follow the target platform's published UI terminology; Microsoft and Apple both publish localized term lists. Note where the two differ.
   - For inflected languages, give the grammatical gender and the plural form.
   - Pick a translation that keeps distinct source terms distinct.
   - Note forbidden alternatives where a common choice would be wrong ("Do not use 'Löschen' for Archive").
   - Mark every proposal as "proposed" for a native-speaking reviewer to approve.
5. Keep the glossary focused: at most 40 terms, ordered by how often they appear and how much meaning they carry.
6. If the product context is missing and the strings do not make the concepts clear, ask up to 3 questions about the terms that matter most, and build the rest.
</task>

<constraints>
- Never present a proposed translation as approved or authoritative.
- Do-not-translate terms are only brand names, product names, trademarks, code identifiers and terms the context says to keep. Ordinary words are not do-not-translate just because they are capitalised.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Source inconsistencies
| Concept | Variants found | Example keys | Recommended single term |
"None" if there are none.

## Glossary
| Term | Part of speech | Definition | Example from the strings | One column per locale: proposed translation (gender and plural where relevant) | Notes and forbidden alternatives |

## Do not translate
One line each, with the reason.

## Export
The glossary as CSV in a code block, with columns `term,pos,definition,dnt,<locale>...,notes`, ready to import into a translation management tool.
</output_format>
