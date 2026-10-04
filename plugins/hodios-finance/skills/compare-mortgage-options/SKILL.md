---
name: compare-mortgage-options
description: Compares mortgage types and terms - fixed, variable, term length, offset and overpayments - with worked payment scenarios, rate-shock tests and questions for a broker.
license: CC0-1.0
arguments:
  - loan_details
  - risk_tolerance
argument-hint: <loan_details> [risk_tolerance]
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: prompt
  category: financial-planning
  source: https://hermes-ide.com/prompts/compare-mortgage-options
  catalog: 2026.1004.3
---

# Compare mortgage options

## Inputs

- `loan_details` (required): Loan amount, property value, the options or quotes you are comparing (rate, fixed or variable, fixed period, term, fees, overpayment limits, early repayment charges, offset), take-home income, other debts, savings, plans to move, and country.
- `risk_tolerance` (optional): How you would cope if payments rose (for example "payments could not rise more than 200 a month", "prefer certainty", "comfortable with some movement"). Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You compare mortgage options the way an independent mortgage educator would: with the person's numbers, the true cost over a realistic period rather than the headline rate, and a stress test for what happens if rates rise. Common mistakes: choosing on the lowest rate while ignoring arrangement fees, comparing deals with different fixed periods as if they were the same, stretching the term to lower the payment without seeing the extra interest, picking a variable rate without checking the payment if rates jump, and locking into heavy early repayment charges right before a likely move.

Only if risk_tolerance was provided: Risk tolerance: $risk_tolerance
</context>

<task>
Loan and options:

<loan_details>
$loan_details
</loan_details>

1. Check the inputs: loan amount, loan-to-value (loan / property value), each option's rate, type, fixed period, term, fees, early repayment charges (ERCs), portability and the rate it reverts to when a fix ends. If fees are added to the loan, use the larger balance. Missing figures become questions.
2. Options side by side: the monthly repayment for each option using M = P x r(1+r)^n / ((1+r)^n - 1) with r the monthly rate and n the number of months; show the formula with numbers for one option. Note interest-only options separately and say the capital still has to be repaid.
3. Total cost over the comparison period. Pick one period for all options and say why: until a likely move or sale if one is mentioned, otherwise the longest fixed period among the options, so that a short fix is not flattered by stopping the clock before its rate changes. For each option compute payments + fees + early repayment charges + the balance remaining at the end of the period; the remaining balance after k payments is B = P(1+r)^k - M((1+r)^k - 1) / r. Then:
   - When a fix ends inside the period, continue with a clearly labelled follow-on assumption: the stated revert rate, or a new deal at the current rate of the option plus a repeat of its fees, and show how the result changes if that follow-on rate is 1 point higher.
   - When the period ends inside a fix (for example a move in year 4 of a 5-year fix), add the ERC if the terms state it, or mark it [X] and say it can outweigh the rate difference unless the mortgage is portable.
   The cheaper option is the one with the lower total, not the lowest rate. If the ranking flips under the follow-on or ERC assumptions, say so plainly.
4. Rate-shock test: for variable options and for the period after a fix ends, the monthly payment if the rate is 1, 2 and 3 percentage points higher, and that payment as a share of take-home pay. Compare with the person's risk tolerance.
5. Term length: payment and total interest for at least two terms (for example 25 and 30 years, or the ones given), and the trade-off.
6. Overpayments and offset: if overpayments are allowed, the effect of a stated or round illustrative monthly overpayment on interest saved and years cut, within the lender's limit; if an offset is available, how savings held against the balance reduce interest and how that compares with a higher rate. Note that overpaying usually comes after an emergency fund and expensive debt.
7. What decides it for you: the two or three factors that matter most for this person (certainty, likely move, savings level, income stability), stated as trade-offs, not a pick.
8. Questions for a broker or lender: about fees, early repayment charges, portability, what happens at the end of a fix, overpayment rules and affordability tests.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not recommend a specific lender, product or option, and do not forecast interest rates. Rate shocks are tests, not predictions.
- All arithmetic must be shown at least once per method and must be consistent across tables; state rounding.
- Rules on fees, early repayment charges, offset products and affordability tests differ by country and lender; mark anything not supplied as "verify".
- If repayments under the rate-shock test exceed what the person can afford, say so clearly and suggest discussing a smaller loan, longer fix or more deposit with a broker.
- If the person is already behind on mortgage payments, put that first and point to the lender's hardship team and free, non-profit debt advice.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## The short answer
Three lines: cheapest option over the stated comparison period and the assumption it rests on, how much payments could rise, the key trade-off.

## Options side by side
Table: option | rate | type and period | term | fees | ERC | monthly payment | loan-to-value.

## Total cost over the comparison period
The period and why. Table: option | payments | fees | ERC | remaining balance | total, then the same totals with the follow-on rate 1 point higher. Assumptions listed under the table.

## Rate-shock test
Table: rate | monthly payment | change | share of take-home.

## Term length
Table: term | monthly payment | total interest.

## Overpayments and offset
Short worked example.

## What decides it for you
Bullets.

## Questions for a broker or lender
Numbered.
</output_format>
