---
name: explain-marginal-tax-rates
description: Explains marginal versus effective tax rates with the person's income and supplied brackets, showing why a higher bracket only taxes the extra income and where real cliff edges exist.
license: CC0-1.0
arguments:
  - income
  - brackets
  - country
argument-hint: <income> [brackets] [country]
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: prompt
  category: taxes
  source: https://hermes-ide.com/prompts/explain-marginal-tax-rates
  catalog: 2026.1004.0
---

# Explain marginal and effective tax rates

## Inputs

- `income` (required): Taxable income to work with, with currency and whether it is before or after allowances or deductions (for example "62,000 EUR taxable income" or "salary 48,000, considering a raise to 53,000").
- `brackets` (optional): The bracket table to use, copied from an official source, with the year and country (for example: 0% to 12,570; 20% to 50,270; 40% to 125,140; 45% above). Optional; without it the answer uses clearly made-up brackets.
- `country` (optional): Country (and state or region if it has its own income tax) and tax year, so the answer can name the right official source and any well-known tapers to verify. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You teach how progressive income tax works using the person's own numbers. The most common misunderstanding is that moving into a higher bracket makes all income taxed at the higher rate, so a raise could leave someone worse off. In a bracket system that is false: only the income above each threshold is taxed at that band's rate. But the honest answer has a second half: some systems contain real cliff edges and tapers (an allowance withdrawn as income rises, a benefit or credit reduced, a social contribution with its own thresholds), and there the effective marginal rate on a slice of income can be much higher than the headline bracket.

Income: $income
Only if country was provided: Country and tax year: $country
</context>

<task>
Only if brackets was provided: Brackets to use:

<brackets>
$brackets
</brackets>

1. If brackets were supplied, use exactly those. If the income given is a gross salary and the table applies to taxable income after allowances or deductions, say so: apply only the allowances the person supplied, or label the result approximate. If not, do not guess a real country's current brackets: build a simple, obviously illustrative table (round thresholds and rates), label it "made-up brackets for teaching", explain the concept with it, and tell the person to paste their official bracket table to see their real figures.
2. Tax band by band: split the income across the bands, compute the tax in each, and total it. Show every multiplication.
3. Marginal versus effective: state the marginal rate (the rate on the next unit of income) and the effective or average rate (total tax / income), and explain in two sentences why they differ.
4. What a raise really costs: if a raise or second figure is given, compute the extra tax and the extra take-home on the increase, and the rate on that increase. Otherwise use an extra 1,000 as the example. Make explicit that crossing a threshold only changes the rate on the part above it.
5. Where it gets more complicated: in general terms, list what can make the true marginal rate differ from the bracket rate: social contributions or payroll taxes with their own thresholds, allowances or credits that phase out, means-tested benefits withdrawn as income rises, student loan repayments based on income, and local or regional taxes. If a country is given or obvious from the input and you are confident a well-known taper exists there, mention it as an example to verify; otherwise stay general.
6. What to check: where to find their official bracket table and what to confirm (year, filing status, allowances applied before the brackets).
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Never present a country's brackets, allowances or thresholds as current fact unless they were supplied. Mark anything you add from memory as "verify".
- All arithmetic must be shown and must add up exactly. Round only the final figures, and say how you rounded.
- Explain income tax only unless the person asks about the other items; mention them in step 5.
- This is an explanation, not a tax calculation for filing; say once that the real liability depends on deductions, credits and status.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## The short answer
Two or three sentences with the marginal rate, effective rate and total tax.

## Tax band by band
Table: band | rate | income in this band | tax. Totals row.

## Marginal versus effective
Two short paragraphs.

## What a raise really costs
Small table: before | after | difference, for income, tax and take-home.

## Where it gets more complicated
Bullets.

## What to check
Bullets.
</output_format>
