---
name: dispute-resolution-track
description: Takes a consumer or tenant dispute from facts and evidence to a complaint letter, an ombudsman or regulator escalation and small-claims preparation, pausing for approval between steps.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: workflow
  category: legal-correspondence
  source: https://hermes-ide.com/prompts/dispute-resolution-track
  catalog: 2026.1003.2
---

# Dispute resolution track

## Inputs

- [DISPUTE] (required): What happened, in order, with dates, amounts, the other party (company, landlord, tradesperson), what was promised, what you have already tried and what you want as a remedy.
- [EVIDENCE] (optional): The evidence you hold, listed - receipts, contracts, emails, chat logs, photos, call notes with dates. Optional at the start; step 1 asks for it.
- [COUNTRY] (optional): Country and region where the dispute is, for example "Scotland" or "California, USA". Optional; step 1 asks if it matters.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Takes one consumer or tenant dispute up the escalation ladder that works in most places: facts and evidence, a formal complaint, a free outside body (ombudsman, regulator, deposit scheme, alternative dispute resolution), and only then small claims. Each step writes one artifact and stops for approval, because the person may settle at any rung. Later steps reuse the approved case summary.

<dispute>
[DISPUTE]
</dispute>
Only if [EVIDENCE] was provided: 
<evidence>
[EVIDENCE]
</evidence>
Only if [COUNTRY] was provided: Country: [COUNTRY]

- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.

Rules for every step:
- Use only facts the person has given or confirmed. Never invent dates, amounts, laws, scheme or regulator names; use [BRACKETS] and keep a list of open questions.
- Name every time limit (complaint, referral, payment dispute, limitation period) as "to verify locally", earliest first.
- Do not predict whether the person will win.
- For personal injury, discrimination, employment, eviction, debts already at court or large sums, say early that a lawyer, legal aid or specialist advice service should look at it first.
- Keep everything the other side or an outside body will read factual and calm: no threats, insults or exaggeration.
- The remedy is what the facts and evidence support (a refund, repair, replacement, the cost of putting it right, or proven losses), with its calculation. Do not add sums for distress or penalties unless the person can point to a basis, and mark any such item "to verify".
- If the person asks to skip a step, say in two lines what skipping usually costs (outside bodies and courts commonly expect a formal complaint first, and costs or claims can suffer without one), then run the step they ask for only once they confirm. Skipping a step never removes the rules above.

## Steps

Work through these steps in order. Do not skip a gate.

1. case (discover)
2. complaint (build)
3. escalate (ship)
4. claim (plan)

### Step 1: Build the case summary

1. Ask for anything that changes the route and is missing: country and region, how it was paid (card, transfer, cash, payment service), whether there is a written contract or tenancy, and whether a formal complaint was already made.
2. Write a dated timeline (date, event, which evidence shows it) and an evidence index (item, what it proves, held or still to get). Suggest evidence still worth gathering: screenshots of the listing or terms, photos, dated notes of calls, bank statements.
3. State the dispute in two sentences, and the remedy precisely with the amount and how it is calculated. Flag any part the evidence does not support.
4. Name the other party correctly (legal name, agent, platform or deposit holder) or mark it [TO CONFIRM].
5. List the escalation routes that commonly exist for this kind of dispute, each with any time limit you know, all marked "to verify locally".

Sections: Timeline, Evidence, The dispute, Remedy, Other party, Routes and time limits, Open questions, Get advice first if.

Stop and wait for approval and answers.

Save this step's result to `dispute/01-case-summary.md`.

**Gate:** stop here and wait for the user's approval before step 2 (complaint).

### Step 2: Write the formal complaint

Using only the approved case summary, write a one-page formal complaint (outside bodies usually expect the business to have had one):

- Subject line with the reference and "Formal complaint".
- The facts as numbered paragraphs in date order, with evidence listed as attached.
- Why the remedy is due, by reference to what was promised, the terms, or the goods or service not being as agreed; rights in general terms unless the person cites a law.
- The exact remedy and amount, a deadline as a calendar date (14 days unless a local rule suggests otherwise), a request for a final written response, and that the matter will go to an outside body if unresolved.

Add a sending plan (complaints contact, proof of delivery, copy kept, deadline in the calendar). If payment was by card or a payment service, add: ask the provider about a payment dispute now, in parallel, as those windows can be short.

Sections: Letter, Sending plan, Parallel actions.

Stop. The person comes back with the reply, or when the deadline passes.

Save this step's result to `dispute/02-complaint-letter.md`.

**Gate:** stop here and wait for the user's approval before step 3 (escalate).

### Step 3: Escalate to an outside body

Ask for the reply (or confirmation that none came) before writing anything.

1. Summarise the response, quoting it. If an offer was made, set out plainly what accepting it would mean; do not tell the person whether to accept.
2. For each candidate route (ombudsman, regulator, deposit scheme dispute service, alternative dispute resolution, consumer agency, payment dispute), say in general terms what it can do (decide and award, mediate, or only record complaints), whether it is free and what it needs. Mark names and rules "to verify on the official website". Agree the route with the person.
3. Draft the submission to fit typical form fields: summary, what went wrong, what was asked and answered, remedy sought, attachments.
4. List referral time limits, earliest first, as "to verify".

Sections: Their response, Route options, Submission draft, Time limits.

Stop. Step 4 is only needed if this route fails or is not available.

Save this step's result to `dispute/03-escalation.md`.

**Gate:** stop here and wait for the user's approval before step 4 (claim).

### Step 4: Prepare for small claims

Run only when the earlier routes failed or the person has decided to go to court.

1. Fit check, each "to verify with the court": amount within the local small-claims limit, other party identifiable with an address for service, realistic chance of collecting if they win.
2. If a letter before claim is expected locally, draft it: claim, amount, deadline, and that proceedings may follow without further notice.
3. Prepare a neutral statement of claim in numbered paragraphs, the amount with its calculation, and an evidence bundle index in date order.
4. List what to ask the court or its help desk: filing method, fee and waivers, forms, service, what happens if there is no response, and the limitation period.
5. Hearing prep: the three points that matter most, the evidence for each, and the factual answer to each likely counter-argument.

Say that outcomes cannot be predicted, and suggest a free advice service or one-off lawyer consultation before filing, especially if the other side has a lawyer or counterclaims.

Sections: Fit check, Letter before claim, Statement of claim, Evidence bundle, Check with the court, Hearing prep.

Save this step's result to `dispute/04-small-claims-prep.md`.
