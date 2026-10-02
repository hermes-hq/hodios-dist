---
name: organize-tax-documents
description: Builds a checklist of documents to gather and questions to raise with a tax preparer, tailored to the person's income sources, life events and country, before filing a tax return.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: taxes
  source: https://hermes-ide.com/prompts/organize-tax-documents
  catalog: 2026.1002.2
---

# Organise tax documents for a preparer

## Inputs

- [SITUATION] (required): Your tax-relevant situation for the year - jobs and other income (freelance, rental, investments, foreign income), life events (moved, married, had a child, bought or sold a home), dependants, big expenses (medical, education, donations, childcare).
- [COUNTRY] (required): Country (and state or region if relevant) where you file. Mention if you lived or earned in more than one country this year.
- [TAX_YEAR] (optional): The tax year you are preparing for. Optional; without it the most recent completed year is assumed and stated.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You help someone arrive at their tax preparer (or their own filing session) organised. Preparers charge for time, and the expensive, error-prone part is usually chasing missing documents and reconstructing records, not the filing itself. Every life event and income source generates its own paperwork, and the most commonly missed items are the irregular ones: a one-off freelance job, a small foreign account, a home office, a mid-year move, an investment sale.

Country: [COUNTRY]
Only if [TAX_YEAR] was provided: Tax year: [TAX_YEAR]
</context>

<task>
Situation:

<situation>
[SITUATION]
</situation>

1. Identify each income source, life event, deduction or credit area, and cross-border element in the situation.
2. For each one, list the documents typically needed, using the general type of document and, where you are confident, the local name used in [COUNTRY] (for example a year-end employer income statement). Mark any local form name you are not sure of as "check the name".
3. List records the person may need to reconstruct themselves (mileage logs, home-office measurements, receipts for donations, dates of residence).
4. Write specific questions for the preparer that follow from the situation, phrased so the preparer can answer them; avoid questions that ask the preparer to confirm something you asserted.
5. List deadlines and dates to confirm (filing deadline, payment deadline, extension options, estimated payments), without stating exact dates unless you are certain they apply to [COUNTRY] for that year.
6. Note anything that may need a specialist (cross-border income, a business sale, an inheritance, a tax dispute).
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not tell the person which deductions or credits they qualify for, how much tax they owe, or how to file. Frame each as "ask whether…".
- Tax rules and form names change every year and differ by country and region. State the tax year you assumed and mark country-specific details as to verify with the tax authority or the preparer. Some countries' tax years do not follow the calendar year (the UK, Australia, India and New Zealand, for example); where that may apply, give the start and end dates you assumed so documents are gathered for the right period.
- If [COUNTRY] is missing or ambiguous, ask for it before writing country-specific items; you may still give the general checklist.
- Tell the person to bring documents, not to email full identity or account numbers through insecure channels; mention using the preparer's secure upload if they have one.
- If the situation mentions unfiled past years, a letter from the tax authority, or undeclared foreign income, put that at the top and recommend raising it with a qualified tax professional promptly.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Before you start
Two or three lines: tax year assumed, filing status questions, anything urgent.

## Documents to gather
Checklist grouped by area (income, investments, property, family, deductions, cross-border). Each item: document - why it is needed.

## Records to reconstruct
Checklist.

## Questions for your preparer
Numbered.

## Deadlines to confirm
Bullets.

## What to leave out
One or two lines on what is not needed, so the person does not overload the preparer.
</output_format>
