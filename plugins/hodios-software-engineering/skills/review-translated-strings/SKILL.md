---
name: review-translated-strings
description: QA-checks a translated catalog against its source for placeholder mismatches, broken syntax, truncation risk, terminology drift and untranslated strings. Use before merging translations.
license: CC0-1.0
arguments:
  - source_catalog
  - translated_catalog
  - glossary
argument-hint: <source_catalog> <translated_catalog> [glossary]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: localization
  source: https://hermes-ide.com/prompts/review-translated-strings
  catalog: 2026.1003.0
---

# QA a translated string catalog

## Inputs

- `source_catalog` (required): The source-language catalog, including comments and length limits.
- `translated_catalog` (required): The translated catalog to check, in the same format.
- `glossary` (optional): Approved term translations and do-not-translate terms. Leave empty to check only internal consistency.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Translation QA catches the defects that crash or embarrass the app before users see them. In rough order of cost: a renamed or dropped placeholder that throws at runtime or prints `{name}`, broken ICU or file syntax that fails the whole catalog, missing keys that fall back to English mid-screen, a label too long for its button, and the same product term translated three different ways. Judging fluency is secondary and needs a native speaker. Mechanical checks must be exhaustive.
</context>

<task>
Check the translation against the source.

Source:
$source_catalog

Translation:
$translated_catalog

Glossary: $glossary

Work through every key. Do not sample.
1. **Coverage:** keys missing from the translation, extra keys not in the source, empty values, and values identical to the source. For identical values, decide whether they are legitimate (brand names, "OK", codes, true cognates) or untranslated.
2. **Placeholders:** the same set of placeholders, by name and count: printf (`%s`, `%d`, `%1$s`), ICU arguments, and markup or inline tags. Check that the types match (`%d` was not turned into `%s`) and that positional specifiers are used when arguments were reordered.
3. **ICU and plurals:** argument names and keywords are untouched, `other` is present, and the plural categories match the target locale's CLDR rules (no required category missing, no invalid one added).
4. **Syntax:** the file still parses (JSON escaping, PO quoting and `msgstr[n]` count against `Plural-Forms`, XLIFF well-formed, unbalanced ICU apostrophes or braces).
5. **Length:** values over a declared maximum length, and for short UI labels (under about 25 characters) values more than about 1.5 times the source length. Mark these as truncation risks.
6. **Terminology:** glossary terms translated as approved, do-not-translate terms left as they are, and the same source term translated the same way across keys.
7. **Mechanics:** leading and trailing whitespace, ending punctuation that differs (colons, ellipses, question marks), numbers or dates hard-coded in the text that differ from the source, and a mix of formal and informal address.
8. **Meaning:** flag only clear errors (opposite meaning, wrong object, a dropped negation), each with a confidence level. Leave style preferences out.
</task>

<constraints>
- Severity: **blocker** for anything that can crash, fail to parse or show raw placeholders; **major** for missing translations, wrong meaning, glossary violations and length overflows; **minor** for punctuation, whitespace and consistency.
- Quote the exact source and translated text for every finding, and give a corrected value when you can.
- If the two files are in different formats or clearly do not correspond, say so and stop.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
One line: ship / ship after fixes / do not ship. Then counts by severity, and the number of keys checked.

## Findings
| Key | Check | Severity | Source | Translation | Suggested fix |
Blockers first.

## Could not verify
Strings whose correctness depends on UI context or native-speaker judgement, one line each.
</output_format>
