<context>
Internationalisation bugs hide until the first non-English locale ships. Then a Polish user reads "5 plik" because the code assumed one-or-many plurals, a German button overflows, a Turkish user cannot log in because `"I".toLowerCase()` is not "ı", an Arabic layout is mirrored everywhere except the margins, a Japanese price shows two decimals, and a date reads 03/04 to someone who expects 4 March. The review must find these in the code before translators start, and show the exact input that breaks.
</context>

<task>
Review this code for internationalisation readiness:

[CODE]

Target locales: [TARGET_LOCALES] (if empty, use German, Japanese, Arabic, Polish, Turkish and Hindi as stress cases).

Check each category below. For every finding, construct the locale and input that breaks it.
1. **Strings:** hard-coded user-facing text; concatenation or interpolation that fixes word order; sentence fragments assembled in code; one key reused in different contexts; text baked into images or SVGs.
2. **Plurals and gender:** `count === 1` ternaries, `+ "s"`, and any logic that assumes two forms; messages that assume a grammatical gender.
3. **Dates and times:** fixed format strings, `toString()` or formatting without an explicit locale, assuming the week starts on Sunday or Monday, the 12- versus 24-hour clock, time zone handling (store UTC, display in the user's zone), and non-Gregorian calendars if the targets need them.
4. **Numbers and currency:** `toFixed`, hand-made thousands separators, a hard-coded currency symbol or position, currency minor units (JPY has 0, KWD has 3), floats for money, and parsing user input as if it were always `1,234.56`.
5. **Text handling:** case mapping without a locale (Turkish dotted and dotless i), `length` or slicing that splits surrogate pairs or grapheme clusters (emoji, Indic scripts), byte-based truncation, sorting without a collator, and search that ignores accents or normalisation (NFC versus NFD).
6. **Layout:** fixed widths or heights on text containers (German and Finnish run 30 to 40 percent longer, and short labels can double), truncation without a tooltip, and fonts or line-height that clip scripts with tall glyphs.
7. **Direction (if any target is right-to-left):** physical CSS properties (`margin-left`, `left`, `text-align: left`), directional icons, missing `dir` and `lang` attributes, and user content not isolated with `dir="auto"` or `bdi`.
8. **Locale plumbing:** how the locale is chosen, the fallback chain, `lang` on the document, server-rendered and email text, and locale-sensitive validation (postal codes, phone numbers, names split into first and last).
</task>

<constraints>
- Report only real defects in the given code, each with file and line and the breaking example. Do not list general advice the code already follows.
- Rank by user impact: wrong data or blocked flows (wrong money amount, failed login, corrupted text) first, then unreadable or broken UI, then polish.
- At most 15 findings. If one cause repeats, report it once and list every location.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Summary
Two or three sentences: readiness for the target locales, and the top blockers.

## Findings
Numbered, highest impact first. Each:
- `path:line`: the problem
- Breaks in: the locale and input, with the wrong output it produces
- Fix: the code change, using the platform's locale-aware API (for example `Intl.NumberFormat`, `Intl.PluralRules`, `Intl.Collator`, ICU MessageFormat, or the platform formatter)

## Looks fine
Categories checked with no issues, in one line.
</output_format>
