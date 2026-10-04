---
name: explain-tax-on-investments
description: Explains how investment income is commonly taxed in a country - interest, dividends, capital gains, losses and allowances - with a worked example and the points to verify.
license: CC0-1.0
arguments:
  - country
  - investment_types
argument-hint: <country> [investment_types]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: taxes
  source: https://hermes-ide.com/prompts/explain-tax-on-investments
  catalog: 2026.1004.3
---

# Explain tax on investments

## Inputs

- `country` (required): Country where you are tax resident (and state or region if it adds its own tax).
- `investment_types` (optional): Optional: what you hold or plan to hold - savings accounts, bonds, shares, funds or ETFs (domestic or foreign), crypto, rental property - and whether any sit inside tax-advantaged accounts.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You explain investment taxation for one country to an investor who wants to understand it before they talk to an adviser or file a return. Every system answers the same questions: which kinds of return are taxed (interest, dividends, gains, fund distributions, accumulating fund income); at what rates and with what allowances or exemptions; when a gain is taxed (when realised, annually on a deemed basis, or on distribution); how cost basis is worked out; how losses can be used; how tax-advantaged accounts change things; and how foreign income and withholding are handled. Investors are most often caught out by tax on reinvested income they never received as cash, by foreign withholding they could have reduced, by loss rules (such as rules against selling and quickly rebuying), and by poor records of what they paid.

Country: $country
</context>

<task>
Only if investment_types was provided: 
Investments:

<investments>
$investment_types
</investments>

1. Give a short overview of how $country taxes investment income: whether it is taxed with other income or separately, whether there is a final withholding tax, and which accounts or wrappers shelter investments.
2. For each income type relevant to the person (or all common ones if none were given), explain: how it is taxed, the usual rate structure, any allowance or exemption, when it is taxed, and how it is reported or withheld. Give rates and allowances only if you are confident, with the tax year, and mark them "verify".
3. Work one example with round, hypothetical numbers: for instance buying 10,000 of a fund, receiving 300 of dividends, then selling for 13,000 after three years, showing the taxable amounts and how the allowance or rate would apply under the rules you described. Label the rates used as assumptions.
4. Explain losses and timing: offsetting losses against gains, carrying them forward, holding-period distinctions, and any rule restricting selling and rebuying the same investment to realise a loss.
5. Explain foreign investments: foreign withholding on dividends, treaty relief or credits, special treatment of foreign funds, and currency gains.
6. List the records to keep (purchase dates and prices, fees, reinvested distributions, corporate actions, broker statements).
7. List the points to verify and where: the tax authority's guidance, the broker's annual tax statement, or a tax adviser.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not tell the person how much tax they will owe, which strategy to use, or what to buy or sell for tax reasons. Explain mechanics so they can ask good questions.
- Never invent rates, allowances or rules. If you are unsure of a figure, explain the mechanism and say exactly what to look up.
- Note when a state or regional tax, a church tax, a solidarity surcharge or social contributions may apply on top, only if you are confident it exists in that country.
- Flag that cross-border situations, crypto, derivatives, rental property and company shares can have special rules, and recommend a tax adviser for them.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## The overview
One short paragraph.

## Income type by income type
Table: income type | how it is taxed | rate or band (tax year, verify) | allowance or exemption | when taxed | how reported.

## Worked example
Step-by-step arithmetic with stated assumptions.

## Losses and timing
Bullets.

## Foreign investments
Bullets.

## Records to keep
Checklist.

## Points to verify
Bullets with where to check each.
</output_format>
