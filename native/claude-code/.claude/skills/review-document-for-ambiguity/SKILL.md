---
name: review-document-for-ambiguity
description: Finds statements in instructions, policies, requirements or agreements that readers could interpret two ways, explains each reading and its consequence, and proposes unambiguous wording.
license: CC0-1.0
arguments:
  - document
  - reader
  - document_type
argument-hint: <document> [reader] [document_type]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: editing
  source: https://hermes-ide.com/prompts/review-document-for-ambiguity
  catalog: 2026.1004.1
---

# Review a document for ambiguity

## Inputs

- `document` (required): The text to review, such as a policy, procedure, instructions, requirements, terms, a brief or an agreement.
- `reader` (optional): Who has to act on it, for example "new warehouse staff", "a contractor building the feature" or "tenants".
- `document_type` (optional): What kind of document it is, for example "expenses policy", "software requirements", "assembly instructions", "service agreement".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Ambiguity is cheap to fix on the page and expensive to discover later, in a dispute, a wrong build or an inconsistent decision. Authors cannot see their own ambiguities because they know what they meant. A useful review reads as the least charitable competent reader would, finds statements with two or more plausible readings, shows the readings side by side with what each would lead someone to do, and offers wording that allows only the intended one.

Common sources of ambiguity to check:
- **Lexical:** a word with two meanings ("bi-weekly", "sanction", "next Friday"), or an undefined term.
- **Inconsistent terms:** the same thing called two names, or one name used for two things.
- **Scope and attachment:** what a modifier or condition applies to ("employees and contractors with a laptop"); "and" versus "or"; "and/or".
- **Quantifiers and negation:** "all … not", "up to", "at least", "a few", "regularly".
- **Time:** "within 30 days" (calendar or business, from when), "by Friday" (inclusive, which time zone), "annually".
- **Reference:** "it", "they", "this", "the above", "the manager" when several are in play.
- **Modal strength:** "should", "may", "will", "must" used interchangeably for obligations.
- **Missing actor:** passive voice that hides who must act ("requests will be approved").
- **Vague standards:** "reasonable", "promptly", "where possible", "appropriate" with no test.
- **Conditions and exceptions:** nested if, unless, except, and which takes precedence when two rules conflict.
</context>

<task>
Review the document below for ambiguity.Only if document_type was provided:  Document type: $document_type.Only if reader was provided:  The reader who must act on it: $reader.

<document>
$document
</document>

1. If the document is empty, ask for it and stop. If no reader is given, assume a competent reader who was not involved in writing it and say so in the Summary.
2. Read the whole document once for purpose. Then go statement by statement looking for the sources listed above.
3. For each ambiguity, record: the location (section or a few quoted words), the exact quoted text, the type, reading A and reading B (and C if needed), the practical consequence of the difference for the reader, a severity, and proposed wording.
   - **High:** readers would act differently in ways that cost money, safety, rights, deadlines or a failed delivery.
   - **Medium:** likely to cause questions, delays or inconsistent handling.
   - **Low:** unlikely to mislead in practice but worth tightening.
4. Proposed wording must allow only the intended reading. If you cannot tell which reading the author intended, give wording for each and ask.
5. List terms that should be defined once and used consistently, with a suggested definition where the document implies one, or a question where it does not.
6. Do not flag ordinary style issues, typos or wordiness unless they create ambiguity.
</task>

<constraints>
- Quote the document exactly; never paraphrase it in the "text" column.
- Report only genuine ambiguities with two plausible readings, not far-fetched ones. Fewer, real findings beat a long list.
- Keep proposed wording as close to the original as possible and in the document's register.
- If the document is a contract or other legal text, note once that this is a drafting clarity review, not legal advice, and that changes to binding terms should be checked by someone qualified.
</constraints>

<output_format>
## Summary
Two or three sentences: how many ambiguities by severity, the most consequential one, and the assumed reader.
## Ambiguities
Table: # · Location · Text · Type · Reading A · Reading B · Consequence · Severity · Proposed wording. Ordered by severity, then position.
## Terms to define
Table: Term · Where used · Problem · Suggested definition or question.
## Notes
Bullets: patterns across the document (for example "uses 'should' for both rules and advice") and any author questions. "None" if none.
</output_format>

<examples>
Text: "Expenses must be submitted within 30 days with receipts over 25 EUR."
Reading A: submit all expenses within 30 days; attach receipts only for items over 25 EUR.
Reading B: the 30-day rule applies only to expenses over 25 EUR, which need receipts.
Proposed: "Submit every expense within 30 calendar days of the purchase date. Attach a receipt for any item over 25 EUR."
</examples>
