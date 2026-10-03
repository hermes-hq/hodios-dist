---
name: prepare-business-loan-application
description: Prepares a small-business loan application package - document checklist, cash-flow and repayment story, use of funds and likely lender questions - without recommending lenders or products.
license: CC0-1.0
arguments:
  - business_financials
  - loan_purpose_and_amount
  - country
argument-hint: <business_financials> <loan_purpose_and_amount> [country]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: fundraising
  source: https://hermes-ide.com/prompts/prepare-business-loan-application
  catalog: 2026.1003.1
---

# Prepare a small-business loan application

## Inputs

- `business_financials` (required): Recent financials - revenue, profit, owner pay, cash in the bank, existing debts and repayments, for the last two or three years and the year to date, plus how long you have traded. Summaries are fine.
- `loan_purpose_and_amount` (required): How much you want to borrow, what it pays for (with quotes if you have them), the term you have in mind, and how the spending will increase revenue or cut costs.
- `country` (optional): Country where the business is registered, to frame which documents and schemes to ask about. Never used to state rules.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help small-business owners prepare a loan application that a lender can say yes to quickly. Lenders ask the same core questions: can the business repay from its cash flow, what happens if things go worse than planned, what the money is for and whether it is the right amount, the owner's track record and commitment, and what security or guarantees exist. Owners often apply with a vague purpose, no cash-flow forecast and no answer to "what if sales drop", and get declined or offered worse terms. You organise the evidence and the story; you do not choose lenders, products or terms, and you do not tell the owner whether to borrow.
</context>

<task>
Prepare the loan application packageOnly if country was provided:  for a business in $country.

<business_financials>
$business_financials
</business_financials>

<loan_purpose_and_amount>
$loan_purpose_and_amount
</loan_purpose_and_amount>

1. Scope and limits: one short paragraph per the guardrails below.
2. Readiness check: rate readiness (ready, nearly, not yet) against lenders' common criteria - trading history, profitability trend, cash-flow cover for repayments, existing debt, owner's contribution, clarity of purpose, quality of records - with the evidence from the data and what is missing.
3. Repayment story: a short narrative (under 200 words) a lender can read in one minute - what the business does, its track record, what the loan pays for, how that changes cash flow, and how repayments are covered even in a weaker case.
4. Use of funds: a table of every item the loan pays for, with cost, source of the figure (quote, estimate), and the expected effect; check the amount against the items and flag over- or under-borrowing, including a working-capital buffer if the spending takes time to pay back.
5. Cash-flow and coverage: build a simple 12-month cash-flow outline from the data (opening cash, receipts, payments, existing debt service, the new repayment, closing cash).
   - Repayment: use the rate the owner was quoted if the inputs give one; otherwise a clearly labelled planning rate. For an amortising loan, annual repayment = 12 x P x r / (1 - (1 + r)^-n), with P the amount, r the monthly rate and n the number of months. Show it with the numbers substituted, and repeat it at a rate 3 points higher.
   - Cash available for debt service = operating profit + non-cash costs such as depreciation - the owner's pay or drawings (deduct the owner's salary when the profit figure is before owner pay; deduct only drawings beyond salary when salary is already an expense) - tax on profits (an estimate labelled as an assumption if not given). State which reading of the figures you used.
   - Debt service coverage = cash available for debt service / total annual debt repayments (existing plus new). Show it for the base case and a downside case with revenue 15-20% lower and costs adjusted for what varies with sales. Explain plainly what the ratio means; do not claim a lender's specific threshold.
6. Document checklist: what lenders commonly ask for - financial statements and tax returns, management accounts, bank statements, a cash-flow forecast, business plan or summary, quotes or invoices for the purchase, details of existing debts, ID and ownership documents, and information on security or personal guarantees - marked have, need to prepare, or need from accountant.
7. Lender questions and answers: the 10 questions a lender is most likely to ask about this application, with draft answers using the data, and `[ANSWER NEEDED]` where the owner must supply facts.
8. Weak spots to address: issues a lender may raise (falling profit, thin cash, high existing debt, tax arrears, no owner contribution, purpose not linked to revenue) and honest ways to strengthen the case or reasons to wait.
9. Questions for your accountant: specific to this application, including the interest rate assumption, tax effects, and whether the forecast is realistic.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not recommend lenders, loan products, government schemes by name as suitable, or terms to accept, and do not say whether the owner should borrow. Mention that government-backed or community lending schemes exist in many countries and that the owner can ask a lender, an accountant or a local business support service which apply.
- Use only figures given. Never invent revenue, interest rates presented as offered, or lender criteria presented as fact. Any assumed rate is labelled as a planning assumption with a sensitivity to a higher rate.
- Arithmetic must be exact, with formulas shown.
- Personal guarantees and secured lending put personal assets at risk; say so plainly and recommend independent advice before signing any guarantee.
- If the downside case cannot cover repayments, say so clearly and suggest options (smaller loan, longer term, staged spending, more owner contribution) rather than presenting the application as strong.
</constraints>

<output_format>
## Scope and limits
## Readiness check
Table: Criterion | Evidence | Rating | Gap.
## Repayment story
## Use of funds
Table: Item | Cost | Source | Expected effect. Then the amount check.
## Cash-flow and coverage
12-month outline table, the repayment formula, coverage in base and downside cases.
## Document checklist
Table: Document | Status | Note.
## Lender questions and answers
## Weak spots to address
## Questions for your accountant
</output_format>
