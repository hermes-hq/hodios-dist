---
name: contract-review-track
description: Reviews a contract in gated steps, from a plain summary to risk flags by severity, questions for the other side, redline priorities and a brief for a lawyer.
license: CC0-1.0
arguments:
  - contract_text
  - your_side
argument-hint: <contract_text> <your_side>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: contracts
  source: https://hermes-ide.com/prompts/contract-review-track
  catalog: 2026.1004.1
---

# Contract review track

## Inputs

- `contract_text` (required): The full contract with clause numbers, plus any schedule, order form or policy it incorporates. Remove bank details and ID numbers.
- `your_side` (required): Which party you are and the deal in a sentence, for example "the supplier, selling 12 months of support for 40,000" or "the tenant of a small shop".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Reviews one contract for one party in the order a careful reviewer works: understand the deal, rank the risks, ask the other side what is unclear, decide what to change, then hand a lawyer a tight brief so their time goes on judgement, not reading. Each step writes one artifact and stops for approval, because answers from the other side or the user can change everything downstream. Later steps build only on approved artifacts.

<contract>
$contract_text
</contract>

Acting for: $your_side

- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.

Rules for every step:
- Quote the contract exactly with clause numbers. Never invent clauses, laws, case law or market figures; write "not stated" for anything absent.
- Do not predict enforceability or outcomes. Where they matter, write "check under the governing law" and carry the point into the lawyer brief.
- Read from the user's side. The same clause can be a protection or a risk depending on who you act for.
- If the user's party is ambiguous or a referenced document is missing, ask in step 1 before going further.
- If the user asks to skip a step, say in one line what the skipped step usually catches, and continue once they confirm.
- Keep every artifact short enough to read in five minutes. Detail goes in tables, not paragraphs.

## Steps

Work through these steps in order. Do not skip a gate.

1. summary (discover)
2. risks (review)
3. questions (review)
4. redlines (build)
5. brief (ship)

### Step 1: Plain summary

1. Confirm the contract type, the parties, which one the user is, effective date, term, governing law and dispute forum. List documents the contract incorporates that were not supplied.
2. Explain the deal in plain language: what each side gives and gets, money and timing, how it ends.
3. List each party's main obligations in a two-column table (us | them) with clause numbers.
4. Note defined terms that change the meaning of ordinary words (for example a narrow "Services" or a broad "Losses").
5. Ask up to five questions whose answers change the review: deal value, how much leverage the user has, what was agreed outside the document, deadlines for signing, and any part already performed.

Sections: The deal, Parties and term, Obligations, Defined terms that matter, Missing documents, Questions for you.

Stop and wait for approval and answers.

Save this step's result to `contract-review/01-summary.md`.

**Gate:** stop here and wait for the user's approval before step 2 (risks).

### Step 2: Risk flags by severity

Using the approved summary and answers, review every clause from the user's side and flag risks:

- High: open-ended or disproportionate exposure, such as uncapped or one-way liability and indemnities, IP wider than the deal, unilateral variation, termination rights only for the other side, auto-renewal with a hard-to-meet notice window, exclusivity or non-compete, personal guarantees.
- Medium: imbalance or vagueness that matters in a dispute, such as undefined acceptance, no cure period, vague service levels, payment terms that strain cash flow, missing confidentiality or data protection terms.
- Low: drafting and clarity issues.

For each flag give the clause, a short quote, what could happen in practice (one-line scenario), and severity. Note protections that are missing for the user's side. Order by severity, then clause.

Sections: Risk table (clause, quote, scenario, severity), Missing protections, Points to check under the governing law.

Stop and wait for approval. The user may re-rank or drop flags.

Save this step's result to `contract-review/02-risk-flags.md`.

**Gate:** stop here and wait for the user's approval before step 3 (questions).

### Step 3: Questions for the other side

From the approved risk flags, write the questions to send before negotiating. Good questions clarify intent and often fix a problem without a redline.

1. Write one question per unclear or medium-to-high item, tied to its clause. Ask what the clause is meant to cover, how it works in practice, or whether the other side would accept a specific clarification.
2. Ask for every missing document named in step 1.
3. Keep the tone neutral and commercial: no accusations, no legal conclusions.
4. Draft a short covering email (under 150 words) that sends the questions as a numbered list and proposes a reply date.

Sections: Questions (numbered, with clause), Documents requested, Covering email.

Stop. The user sends the questions and returns with the answers, or approves moving straight to redlines.

Save this step's result to `contract-review/03-questions.md`.

**Gate:** stop here and wait for the user's approval before step 4 (redlines).

### Step 4: Redline priorities

Using the approved risks and any answers from the other side:

1. Drop flags the answers resolved, and say which.
2. Sort the rest into must-have, trade-able and leave-alone, with at most 10 changes in the first two groups combined.
3. For each must-have and trade-able change: quote the original, show the proposed wording with ~~deletions~~ and **insertions** (smallest edit that works), a one-sentence reason the other side can accept, and a fallback position.
4. Suggest a trade plan: which trade-able items to concede in exchange for which must-haves.

Sections: Resolved by answers, Redline table (clause, change, reason, fallback, priority), Tracked wording, Trade plan, Left alone.

Stop and wait for approval before writing the lawyer brief.

Save this step's result to `contract-review/04-redline-priorities.md`.

**Gate:** stop here and wait for the user's approval before step 5 (brief).

### Step 5: Lawyer brief

Write a one-page brief a lawyer can act on in a short paid review:

- The deal in three lines: parties, value, term, governing law, signing deadline.
- What the user needs from the lawyer: specific questions only, for example "is the cap in 11.2 effective against negligence claims under the governing law?", "is the non-compete in 15 enforceable as drafted?", "does our proposed wording for 9.1 achieve a mutual indemnity?".
- The approved redline priorities, with the clauses and proposed wording attached.
- Points carried forward as "check under the governing law" from earlier steps.
- What has been agreed or answered by the other side so far, with dates.
- Documents attached.

Then add a three-line checklist for the user: what to send the lawyer, how to ask for a fixed-fee quote for a limited review, and the date by which they need the answer.

Sections: Deal, Questions for the lawyer, Proposed changes, Open legal points, History, Attachments, Your checklist.

Save this step's result to `contract-review/05-lawyer-brief.md`.
