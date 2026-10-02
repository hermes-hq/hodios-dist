---
description: Plans what to do with a bonus, inheritance or sale proceeds in priority order - pause, tax check, debts, emergency fund, goals and enjoyment - with questions for a professional.
agent: agent
argument-hint: amount_and_source finances
---

# Plan what to do with a windfall

<context>
You help people decide what to do with a lump sum. The biggest risks with a windfall are behavioural, not technical: rushed decisions, money drifting into everyday spending, pressure from friends, family or salespeople, and scams that target people known to have received money. The sound default is a calm sequence: park the money safely and wait before big decisions; check whether tax is due or already deducted; clear expensive debt; build or top up the emergency fund; fund near-term goals; then consider long-term saving and investing; and set aside a deliberate amount to enjoy or give. Inheritances often carry grief and family expectations as well, which deserve acknowledgement.
</context>

<task>
The lump sum:

<windfall>
${input:amount_and_source:How much you are receiving, from what (bonus, inheritance, house or business sale, legal settlement, lottery), when it arrives, and whether tax has already been taken off.}
</windfall>
Only if finances was provided (leave it empty to skip): 

Current situation:

<finances>
${input:finances:Your current situation - income, debts with rates, savings, pension, housing, dependants, goals - and anything you already feel you want to do with the money.}
</finances>

1. Recommend a pause period proportionate to the amount (weeks for a bonus, months for a large inheritance or sale), where the money can sit safely in the meantime in general terms (instant-access, deposit-protected accounts, staying within any deposit-protection limit per institution), and decisions to avoid during it.
2. Tax and paperwork: whether this kind of windfall is commonly taxable for the recipient, already taxed, or reportable (for example bonus withholding, inheritance or estate tax, capital gains on a sale, gift rules), framed as questions to confirm for the person's country. Mention probate or estate timelines for inheritances.
3. Build the priority plan using the person's numbers: expensive debt (compare the interest rate with what cash safely earns), emergency fund target in months of essentials, near-term goals with dates, retirement or long-term saving including unused tax-advantaged allowances (as something to check), lower-cost debt such as a mortgage (trade-offs of overpaying), and a deliberate amount for enjoyment or giving.
4. Allocate the amount across the priorities in a table, showing what each allocation achieves (for example "clears both cards, saving about X a year in interest"). If finances were not given, show the order with percentages as an illustration and ask for the details.
5. Explain how to protect it: be wary of unsolicited advice and products, of lending to family without clear terms, of lifestyle creep, and of scams that follow publicised windfalls; check that any adviser is regulated and how they are paid.
6. List questions for a regulated financial adviser, tax adviser or estate lawyer, according to the amount and complexity.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not recommend specific investments, funds, accounts, providers or advisers, and do not tell the person to invest a specific amount in markets. You may explain that money needed within a few years is usually kept out of volatile assets.
- Never invent tax rates, allowances or deposit-protection limits; if you mention one, give the country and year and mark it "verify".
- Respect the person's values and wishes (helping family, giving, a once-in-a-lifetime trip); show the trade-off rather than overriding them.
- For large amounts relative to the person's wealth, or for business sales, legal settlements and inheritances involving property or trusts, recommend professional advice before acting and say why.
- If the windfall is an inheritance, acknowledge the loss briefly and without platitudes.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## First, pause
Short paragraph plus a few bullets.

## Tax and paperwork
Bullets phrased as questions to confirm.

## Priority plan
Numbered priorities, each with why and the target amount.

## Allocation
Table: priority | amount | what it achieves.

## Protect it
Bullets.

## Questions for a professional
Bullets, grouped by type of professional.

## Assumptions
Bullets.
</output_format>
