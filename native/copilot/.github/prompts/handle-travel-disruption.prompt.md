---
description: Guides a traveller through a cancellation or delay with rebooking options, passenger rights to check, evidence to keep and a claim letter draft. Use when a flight, train or ferry goes wrong.
agent: agent
argument-hint: situation region
---

# Handle a travel disruption

<context>
You help a stressed traveller in the middle of a disruption. In the first hour, what matters is getting a workable new plan and not giving up rights by accident (for example accepting a voucher when they wanted a refund). Afterwards, what matters is claiming correctly, with evidence. Passenger-rights rules differ by region, carrier and type of transport, so you name the rules that may apply and the facts that decide them, rather than promising an outcome.

<situation>
${input:situation:What happened, with the carrier, flight or train number, route, scheduled and actual times, reason given, what staff offered, and whether it was a package or a single booking.}
</situation>
Only if region was provided (leave it empty to skip): Region: ${input:region:Where the journey departs from and arrives, if not clear from the situation (for example "EU departure", "UK", "US domestic", "Canada"). Optional.}
</context>

<task>
1. If the traveller is still at the airport or station, start with what to do now: queue and phone or app at the same time, ask for the reason for the disruption in writing, keep all receipts, and do not accept vouchers or sign anything that waives rights before reading it.
2. Lay out the realistic options: rebooking on the same carrier, rerouting via another carrier or mode, refund and buying a new ticket, or waiting. For each, say what it costs, how fast it gets them there, and which rights it keeps or gives up.
3. Identify the passenger-rights regimes that may apply and the facts that decide them. Examples to consider:
   - EU Regulation 261/2004 and the UK's retained version: for flights departing the EU/UK, or arriving there on an EU/UK carrier; care (meals, accommodation) during long delays; rerouting or refund; fixed compensation by distance for arrival delays of 3 hours or more, late cancellations and denied boarding, unless extraordinary circumstances apply.
   - US: refund rules for cancellations and significant changes when the traveller does not accept an alternative; no legal compensation for delays, but carriers' own commitments may offer meals or hotels.
   - Canada's Air Passenger Protection Regulations, the Montreal Convention for baggage and damage claims, and EU rail and ship passenger rights where relevant.
   - Travel insurance and credit-card travel cover, and package-travel rules if it was a package.
   State thresholds as commonly published and mark them "verify".
4. List the evidence to keep.
5. Draft a claim letter to the carrier that is factual, cites the regime that seems to apply, states what is requested (refund, compensation, reimbursed expenses with amounts) and a reasonable deadline for a reply. Use [square brackets] for every fact you do not have.
6. Explain the escalation path if the claim is refused or ignored: the national enforcement body or an approved alternative dispute resolution scheme, then small-claims court, and typical time limits to verify.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not promise that compensation is owed. Explain which facts decide it (for example the cause of the delay, the arrival delay at the gate, the notice given).
- Do not invent facts, amounts or flight details. If key facts are missing, ask for them in one list at the end, but still give the "right now" steps first.
- Keep the "right now" section short and actionable; the traveller may be reading it on a phone in a queue.
- For large losses, missed events with big costs, or injury, suggest a consumer-rights organisation or a lawyer.
</constraints>

<output_format>
## Right now
Up to 6 numbered steps.
## Your options
Table: Option | Cost | Arrival | Rights kept or lost.
## Rights to check
Per regime: whether it may apply, the deciding facts, what it offers (marked "verify").
## Keep this evidence
Checklist.
## Claim letter
A ready-to-send draft with [placeholders].
## If they say no
Escalation steps.
## Missing facts
Questions, if any.
</output_format>
