---
description: Categorises a bank or card transaction export into budget categories, totals each one, and flags subscriptions, fees, duplicate charges and spending spikes worth a closer look.
agent: agent
argument-hint: transactions categories
---

# Categorise expenses from a bank export

<context>
You turn a raw bank export into a spending picture someone can act on. Raw descriptions are cryptic ("SQ *BLUE BOTTLE 0423", "AMZN MKTP DE*2X4", "PAYPAL *STEAMGAMES"), sign conventions differ between banks, and transfers between a person's own accounts look like spending unless you take them out. The most useful findings are usually small and recurring: forgotten subscriptions, bank and foreign-transaction fees, duplicate charges, and one category that quietly doubled.

Only if categories was provided (leave it empty to skip): Use these categories, and only add "Uncategorised" when nothing fits:
<categories>
${input:categories:Your own category list, if you have one. Optional; without it a standard household set is used.}
</categories>
</context>

<task>
Transactions:

<transactions>
${input:transactions:Transaction export (CSV or pasted rows) with at least date, description and amount. Remove account numbers and card numbers before pasting.}
</transactions>

1. Detect the format: which column is date, description, amount, and whether debits are negative or in a separate column. State the convention you used.
2. If no category list is given, use: Housing, Utilities, Groceries, Eating out, Transport, Health, Insurance, Subscriptions, Shopping, Entertainment, Travel, Personal care, Kids, Gifts and donations, Fees and interest, Income, Transfers (own accounts), Cash withdrawals, Uncategorised.
3. Categorise every transaction. Use the merchant name, not guesses about what was bought; a supermarket charge is Groceries even if it might include household items. Mark low-confidence matches with "(?)".
4. Exclude income and transfers between own accounts from spending totals, and say how much you excluded. Two cases trip people up:
   - Refunds and reversals reduce the category of the original purchase; they are not income.
   - A payment from a bank account to a credit card is a transfer when the card's own transactions are also in the data (counting both would double-count the spending). If only the bank side is present, show the card payment as its own line, "Credit card payment (contents unknown)", and ask for the card export.
5. Find recurring charges: same merchant at roughly the same amount on a regular interval. Give the monthly and yearly cost.
6. Flag: bank, overdraft, ATM and foreign-transaction fees; interest charges; possible duplicates (same merchant and amount within 3 days); refunds that never arrived for an obvious return; any category or single transaction far above the rest of the period.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Never invent transactions, merchants or amounts. Totals must reconcile: spending by category plus excluded items equals the sum of all rows.
- If the data covers less than a month, say comparisons and "spikes" are limited.
- Do not label any spending as good or bad. Report it and let the person decide.
- If the export contains full account or card numbers, tell the person not to share them and refer to accounts by the last four digits only.
- A flagged duplicate or unknown charge is "worth checking with your bank", not proof of fraud. If several charges look unauthorised, tell them to contact their bank promptly.
- With more than about 200 rows, show the full category totals but list only flagged and low-confidence transactions individually.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Period and totals
Date range, total spending, total income, total excluded transfers.

## Spending by category
Table: category | total | % of spending | number of transactions. Sorted by total.

## Transactions
Table: date | description | amount | category. Low-confidence rows marked "(?)".

## Recurring charges
Table: merchant | amount | frequency | yearly cost | still wanted? (blank for the person to fill).

## Flags
Bullets: fees, possible duplicates, spikes, unknown merchants, each with date and amount.

## Needs your input
Transactions you could not categorise or that need the person to confirm, as a short list.
</output_format>
