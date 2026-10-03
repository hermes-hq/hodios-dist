---
name: format-citations
description: Converts references to APA, MLA, Chicago, Harvard, IEEE or Vancouver, flags missing fields instead of inventing them, and fixes the matching in-text citations. For students and researchers.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/format-citations
  catalog: 2026.1003.1
---

# Format citations in a reference style

## Inputs

- [REFERENCES] (required): The references to format, in any style or as messy notes (author, title, year, journal, DOI, URL…), one per line or as a block.
- [STYLE] (required): The target style and edition if it matters, for example "APA 7", "MLA 9", "Chicago author-date", "Chicago notes-bibliography", "Harvard (my university's guide)", "IEEE", "Vancouver".
- [BODY_TEXT] (optional): Optional text with in-text citations to convert to the same style, for example a paragraph or a whole section.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Citation styles differ in small, rule-bound ways: author name order and initials, where the year goes, sentence case or title case, italics for the journal or the article, "et al." thresholds, DOIs as URLs, ordering of the list (alphabetical for APA, MLA, Chicago and Harvard; by order of first citation for IEEE and Vancouver) and the in-text form (author-date, author-page or numbered). The most damaging mistake is not a misplaced comma but an invented detail: a guessed page range, a DOI that resolves to another paper, or a wrong year. A correct reference with a visible gap is better than a complete-looking wrong one.
</context>

<task>
Format these references in [STYLE].
<references>
[REFERENCES]
</references>
Only if [BODY_TEXT] was provided: 
Also convert the in-text citations in this text to the same style:
<body_text>
[BODY_TEXT]
</body_text>

1. Identify each source's type (journal article, book, chapter, report, website, conference paper, thesis, dataset, software, preprint), because the format depends on it.
2. Format each reference in [STYLE]: names, year or date, title capitalisation, italics (shown with Markdown *italics*), volume, issue, pages or article number, publisher, DOI or URL in the style's form. If the style has variants (Harvard has many institutional versions; Chicago has author-date and notes-bibliography), state which one you used.
3. Wherever a field the style requires is missing or looks wrong (a DOI with the wrong pattern, a page range that runs backwards, a year that does not match a preprint and journal version), insert a visible marker such as [missing: issue] or [check: year] and list it.
4. Order the list as the style requires and detect duplicates.
Only if [BODY_TEXT] was provided: 5. Convert every in-text citation in the body text to the style's form, matching each to its reference. For numbered styles, number by order of first appearance and renumber the list to match. List any citation that has no matching reference, and any reference that is never cited.
</task>

<constraints>
- Never invent or "complete" a DOI, page range, volume, issue, publisher, date or author. Only reformat what is given.
- Do not look up or correct a reference from memory. If something seems wrong, flag it with [check: …] and say why.
- Keep the author's spelling of names, including diacritics and particles (van, de, al-), and apply the style's rule for sorting them.
- If the style named is ambiguous or unknown, say what you assumed.
- Preserve the meaning and wording of the body text; change only the citations.
</constraints>

<output_format>
## Reference list
The formatted list, in the style's order, ready to paste.
## Missing or uncertain details
Table: reference (short) | field | issue | where to find it (for example the journal page, the DOI registry or the library catalogue).
## In-text citations
If body text was given: the revised text, then a list of unmatched citations and uncited references. Otherwise, one example in-text citation per reference in the style.
</output_format>
