---
name: write-file-parser
description: Writes a streaming parser and validator for CSV, log, fixed-width or custom text files that reports malformed records with line numbers instead of crashing. Use for messy input files.
license: CC0-1.0
arguments:
  - sample
  - format_notes
  - language
argument-hint: <sample> [format_notes] [language]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/write-file-parser
  catalog: 2026.1004.1
---

# Write a streaming file parser

## Inputs

- `sample` (required): A representative sample of the file, ideally with a few bad lines. Remove real personal data first.
- `format_notes` (optional): Anything known about the format, such as a spec, field meanings, encoding, the producing system or known quirks.
- `language` (optional): Implementation language. Leave empty to choose one and say why.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Real input files are never as clean as the sample suggests. Quoted CSV fields hold commas and newlines, so a line is not a record. Files arrive with a byte-order mark, CRLF endings, Latin-1 bytes, a trailing delimiter or a truncated last line. A parser that throws on the first bad record and loses the line number makes someone grep a 2 GB file by hand. The parser must stream, keep going, and say exactly what was wrong and where.
</context>

<task>
Write a parser and validator in $language (if empty, pick one suited to the job and say why) for files like this sample:

$sample

Known format notes: $format_notes

1. Infer the format and write it down as a spec before coding: record boundary, field delimiter or column positions, quoting and escaping, header row, encoding, line endings, and each field's name, type, required or optional status, and allowed values or ranges. Mark each item as stated (from the notes), observed (from the sample) or assumed.
2. If a structural question cannot be answered from the sample and notes (for example, whether fixed-width columns count bytes or characters, or whether a field may contain the delimiter), list it, state the assumption you will code to, and continue.
3. Implement a streaming parser that reads incrementally, uses constant memory, and yields one result per record: either a typed record or an error.
   - For CSV-like formats, use the language's real CSV library rather than splitting on commas, and track the physical line where each record starts.
   - For log lines, use one anchored pattern per line type, and join continuation lines such as stack traces onto their record.
   - For fixed-width formats, slice by the documented unit and trim as the spec says.
4. Validate each record against the spec: field count, types, ranges, enums, required fields, and cross-field rules from the notes. Parse dates with explicit formats and time zones, and decimals without float rounding when they are money.
5. Errors must carry the line number, field name or column, a reason a human can act on, and a truncated excerpt of the raw text. Keep going after errors. Offer a strict mode that stops at the first error and an option to stop after N errors.
6. Handle these without crashing: an empty file, a header only, blank lines, a byte-order mark, CRLF, invalid bytes for the encoding (report the offset), a missing final newline, extra or missing columns, and a truncated last record.
7. Write tests from the sample plus one crafted bad line for each error type, and a test that streams a large generated input without loading it all into memory.
</task>

<constraints>
- Never silently coerce or drop a bad value. It is either valid or reported.
- Keep the parsing core free of I/O so it can be tested with strings.
- Do not echo whole records containing personal data in errors; truncate excerpts.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Format spec
| Field | Position or column | Type | Required | Rule | Source (stated / observed / assumed) |
Then record boundary, encoding and quoting in a few lines.

## Questions and assumptions
Numbered, or "None".

## Code
Complete code in one or more code blocks.

## Tests
Code, then one line per test explaining what it proves.

## Sample run
What the parser yields for the given sample: the record count, then each error with its line number and reason.
</output_format>
