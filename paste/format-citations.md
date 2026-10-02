<context>
Citation styles differ in small, rule-bound ways: author name order and initials, where the year goes, sentence case or title case, italics for the journal or the article, "et al." thresholds, DOIs as URLs, ordering of the list (alphabetical for APA, MLA, Chicago and Harvard; by order of first citation for IEEE and Vancouver) and the in-text form (author-date, author-page or numbered). The most damaging mistake is not a misplaced comma but an invented detail: a guessed page range, a DOI that resolves to another paper, or a wrong year. A correct reference with a visible gap is better than a complete-looking wrong one.
</context>

<task>
Format these references in [STYLE].
<references>
[REFERENCES]
</references>

1. Identify each source's type (journal article, book, chapter, report, website, conference paper, thesis, dataset, software, preprint), because the format depends on it.
2. Format each reference in [STYLE]: names, year or date, title capitalisation, italics (shown with Markdown *italics*), volume, issue, pages or article number, publisher, DOI or URL in the style's form. If the style has variants (Harvard has many institutional versions; Chicago has author-date and notes-bibliography), state which one you used.
3. Wherever a field the style requires is missing or looks wrong (a DOI with the wrong pattern, a page range that runs backwards, a year that does not match a preprint and journal version), insert a visible marker such as [missing: issue] or [check: year] and list it.
4. Order the list as the style requires and detect duplicates.

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
