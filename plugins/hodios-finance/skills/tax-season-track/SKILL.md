---
name: tax-season-track
description: Takes a household or freelancer through tax season - document gathering, income and deduction questions, a preparer brief and a post-filing checklist - pausing for approval between steps.
license: CC0-1.0
arguments:
  - situation
  - country
argument-hint: <situation> <country>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: taxes
  source: https://hermes-ide.com/prompts/tax-season-track
  catalog: 2026.1003.2
---

# Tax season track

## Inputs

- `situation` (required): Who is filing (single, couple, family), income sources (salary, freelance, rental, investments, pensions, benefits, foreign income), life events this year (move, marriage, baby, new job, property sale), and whether you use a preparer or file yourself.
- `country` (required): Country (and state or region if relevant) where you file, and the tax year.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Takes this household or freelancer through tax season the way a well-run preparer's intake process does: collect the right documents early, surface every income source and possible deduction as a question rather than a guess, hand the preparer (or the person filing themselves) a clean brief, then close the year properly so next year is easier. Each step writes one artifact and stops for approval; later steps reuse confirmed answers instead of asking again.

<situation>
$situation
</situation>

Country and tax year: $country

- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.

Rules for every step:
- This track organises and explains. It does not compute the final liability, choose a filing position or fill in a return. Decisions go on the list for the preparer or tax adviser.
- Use only facts the person gave or confirmed. Missing items are marked [X] with where to find them; never assume an income source, deduction or figure.
- Mark every deadline, threshold, allowance and form name as "verify" unless you are confident it is current for $country and that tax year; if you do not know the system well, say "I don't know" for that part and keep it general.
- Tell the person to remove identity numbers, tax reference numbers, account numbers and passwords before sharing documents.
- Never help hide income, invent or inflate expenses, or alter records. If asked, decline and steer back to an honest return.
- If the person mentions unfiled past years, a tax debt they cannot pay, an audit, or foreign income or residence changes, flag it in the step where it appears and recommend a tax professional early.
- Keep a running list of open questions and items for the preparer, carried into step 3.

## Steps

Work through these steps in order. Do not skip a gate.

1. documents (discover)
2. income-and-deductions (review)
3. preparer-brief (plan)
4. post-filing (ship)

### Step 1: Documents

1. Confirm the filing unit, the tax year and its key deadlines (filing, payment, any extension route), each marked "verify" unless confident. Work back to a personal target date about three weeks earlier.
2. Build the document checklist from the situation: income documents per source (employer year-end statements, freelance invoices and bank records, rental statements, investment and interest statements, pension and benefit statements, foreign income), deduction and credit evidence to ask about (pension contributions, charitable gifts, childcare, education, medical, home office, business expenses), life-event documents (property purchase or sale, marriage, birth, move), and last year's return and any letters from the tax authority.
3. For each document, say where it usually comes from and when it usually arrives, and mark it have, waiting or missing.
4. Suggest one folder structure and a naming convention so everything is findable.

Sections: Key dates, Document checklist (table: document | source | usually arrives | status), Folder set-up, Open questions. Stop for approval.

Save this step's result to `tax-season/01-documents.md`.

**Gate:** stop here and wait for the user's approval before step 2 (income-and-deductions).

### Step 2: Income and deductions

1. Income inventory: list every income source with the amount from the documents (or [X]), whether tax was already withheld, and anything unusual (a one-off payment, foreign income, a sale of assets, crypto disposals). Check totals against bank records where the person gave them, and flag gaps.
2. Freelance or business income, if any: income minus expenses by category, with expenses that look personal or capital in nature flagged as questions for the preparer, not decided.
3. Deductions and credits to ask about: a list tailored to the situation, each as a question with the evidence needed. Do not say whether the person qualifies; say what decides it.
4. Payments already made: withholding, advance or estimated payments, and any balance from last year.
5. A rough direction only if the figures are complete and the person asks: likely to owe or likely to get a refund, with the reasoning and a clear statement that the preparer's calculation decides.

Sections: Income inventory (table), Business income and expenses (if any), Deductions and credits to ask about, Payments already made, Open questions. Stop for approval.

Save this step's result to `tax-season/02-income-and-deductions.md`.

**Gate:** stop here and wait for the user's approval before step 3 (preparer-brief).

### Step 3: Preparer brief

1. Write a one-page brief for the preparer, or a self-filing checklist if the person files alone: who is filing, the tax year, income sources with totals, documents attached (indexed), life events, changes since last year, and payments already made.
2. List the decisions for the preparer to make, each with the facts they need (for example how to treat a mixed-use expense, whether a deduction applies, filing jointly or separately where that choice exists).
3. List the open questions still unanswered from steps 1 and 2.
4. If self-filing, add a review checklist: totals match source documents, every income source included, bank details for any refund correct, a copy saved before submitting.

Sections: Brief, Decisions for the preparer, Open questions, Self-filing checklist (if relevant). Stop for approval.

Save this step's result to `tax-season/03-preparer-brief.md`.

**Gate:** stop here and wait for the user's approval before step 4 (post-filing).

### Step 4: Post-filing

1. Confirmation: keep the submission receipt, a copy of the return and every document used, and note how long records are usually kept (verify locally).
2. Money: amount due and payment date, or refund expected and how to track it; any advance or estimated payments for next year with dates to confirm; what to do if they cannot pay in full (contact the authority early about a payment arrangement).
3. Next year: changes to make now (withholding or set-aside rate, a separate tax account for freelancers, a receipt routine, a running folder), and life events coming up that will matter.
4. Watch for letters: how to recognise genuine communication from the tax authority and common tax scams.

Sections: Keep these, Payments and refunds, Set up for next year, Watch for. Finish with the date to start next year's track.

Save this step's result to `tax-season/04-post-filing.md`.
