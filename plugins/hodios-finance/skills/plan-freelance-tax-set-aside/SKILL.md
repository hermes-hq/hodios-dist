---
name: plan-freelance-tax-set-aside
description: Estimates what percentage of freelance income to set aside for tax, with every assumption stated, a simple saving routine and a payment calendar to confirm with an accountant.
license: CC0-1.0
arguments:
  - income
  - country
  - expenses
argument-hint: <income> <country> [expenses]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: taxes
  source: https://hermes-ide.com/prompts/plan-freelance-tax-set-aside
  catalog: 2026.1002.2
---

# Plan a freelance tax set-aside

## Inputs

- `income` (required): Expected freelance income for the year (or monthly pattern), plus any salary or other income, and whether income tax or social contributions are already withheld anywhere.
- `country` (required): Country (and state or region if relevant) where you are tax resident, and your business form if known (sole trader, single-member company, other).
- `expenses` (optional): Business expenses you expect to deduct (equipment, software, home office, travel), roughly per year. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help a freelancer avoid the classic first-year shock: spending everything that came in, then facing a tax bill (sometimes plus advance payments for next year) with nothing saved. The goal is a safe set-aside percentage and a routine, not a tax return. Freelancers usually owe more than income tax: social security or national insurance contributions, sometimes health contributions, and possibly sales tax or VAT collected on behalf of the state, which is never the freelancer's money to spend.

Country: $country
</context>

<task>
Income:

<income>
$income
</income>

Only if expenses was provided: Expected business expenses:

<expenses>
$expenses
</expenses>

1. Estimate taxable profit = freelance income minus deductible business expenses. If expenses are not given, assume none and say the set-aside will be conservative.
2. List the charges that typically apply to self-employed people in $country: income tax, self-employed social contributions, any local or regional income tax, and sales tax or VAT if registration thresholds may be crossed. Mark each with your confidence and "verify" where you are unsure of current rates or thresholds.
3. Build an estimate with stated assumptions: rate bands or an effective rate for income tax, contribution rates, and interaction with any salary already taxed. Show the arithmetic and give a range (low, central, high), then round up the central estimate to a simple set-aside percentage of every payment received.
4. Keep any sales tax or VAT collected separate: 100% of it goes into the tax reserve on top of the percentage.
5. Design the routine: a separate account for tax, moving the percentage on the day each payment arrives, and a monthly check.
6. Build a payment calendar of the kinds of payments usually due (annual balance, advance or estimated payments, VAT returns) with "confirm date" next to each, and flag that the first year can include a double payment in some countries.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- This is a cautious planning estimate, not a tax calculation. Say plainly that the real liability depends on details an accountant or the tax authority will confirm, and that rates and thresholds change yearly.
- Never present a rate, threshold or due date as certain unless you are confident it is current for $country; otherwise mark it "verify". If you do not know the country's system well, say "I don't know" for those parts and give the general structure only.
- Err towards setting aside too much rather than too little, and say why.
- Do not advise on tax avoidance schemes, choice of company structure, or which expenses to claim beyond listing common categories to ask about.
- If the person mentions past unpaid tax or an existing bill they cannot pay, tell them to contact the tax authority or a tax professional early about payment arrangements.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Set aside this much
One line: the percentage of each payment (and VAT or sales tax separately, if relevant), plus the estimated annual amount.

## How the estimate works
Table: charge | basis | assumed rate | estimated amount | confidence. Then the low-central-high range.

## Saving routine
Short checklist.

## Payment calendar to confirm
Table: payment type | usual timing | estimated amount | confirm with.

## What could change the number
Bullets.

## Questions for your accountant
Numbered.
</output_format>
