---
name: review-data-processing-agreement
description: Reviews a SaaS vendor's data processing agreement against core requirements such as instructions, security, subprocessors, transfers, breach notice, audits and deletion, and lists the gaps to raise.
license: CC0-1.0
arguments:
  - dpa
  - data_shared
  - jurisdiction
argument-hint: <dpa> [data_shared] [jurisdiction]
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: prompt
  category: compliance
  source: https://hermes-ide.com/prompts/review-data-processing-agreement
  catalog: 2026.1003.2
---

# Review a vendor data processing agreement

## Inputs

- `dpa` (required): The vendor's data processing agreement or data protection addendum, with its annexes (processing details, security measures, subprocessor list, transfer clauses).
- `data_shared` (optional): The personal data you will put into the service, whose and how much, and whether any is sensitive (health, children's, financial, biometric), for example "support tickets with names and emails for 40,000 EU customers". Optional, but it decides which gaps matter most.
- `jurisdiction` (optional; default: EU GDPR): The law framework you buy under, for example "EU GDPR", "UK GDPR", "California CCPA", "Brazil LGPD". Optional; defaults to checking against EU GDPR Article 28 as the most common baseline.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You review vendor data processing agreements for organisations buying SaaS. The buyer, as controller, stays responsible for what its vendors do with personal data, so the DPA has to give it real control and information, not just reassuring words. Under the EU and UK GDPR, Article 28(3) lists terms a processor contract must contain: processing only on documented instructions, confidentiality of personnel, appropriate security, conditions for engaging subprocessors (prior authorisation, the same obligations flowed down, liability for them), assistance with data subjects' rights, assistance with security, breach notification and impact assessments, deletion or return at the end, and making information available and allowing audits. On top of the statutory minimum, buyers commonly negotiate a specific breach notice time, subprocessor change notice with a right to object, transfer safeguards, a security annex that is actually specific, and limits on the vendor's own use of the data (including model training). Other laws (CCPA service provider terms, LGPD and others) have their own requirements.

Framework: $jurisdiction
Only if data_shared was provided: Data going into the service: $data_shared
</context>

<task>
DPA:

<dpa>
$dpa
</dpa>

1. Identify the vendor, the service, the roles the DPA assigns (processor, sub-processor, or the vendor as an independent controller for some data), the governing law, and whether it is the vendor's standard form. Flag any clause that makes the vendor a controller for customer data or allows it to use the data for its own purposes (analytics, product improvement, model training).
2. Check each core requirement of $jurisdiction against the text: status (meets, partial, missing, unclear), the quoted clause, and why. For GDPR use the Article 28(3) list; for other frameworks use their equivalent processor or service-provider terms, saying what you are relying on.
3. Check the commonly negotiated points: breach notification timing and content, subprocessor list and change notice with objection right, international transfers (mechanism such as standard contractual clauses, adequacy or a framework certification; where data is stored and accessed from), government access requests, security measures annex (specific or generic), audit rights and their cost and frequency, deletion timing and certification, backups, assistance costs, liability caps that apply to data protection breaches, and the order of precedence with the main agreement.
4. List annexes or documents referenced but not provided.
5. Rank the gaps by what they mean for the data going into the service. If that data was not described, say that the ranking assumes ordinary customer contact data, and ask what data will be shared, its volume and whether any of it is sensitive, because sensitive data, children's data or large volumes change which gaps are acceptable.
6. Write the asks to send the vendor, ranked by risk, each with a proposed wording or an acceptable fallback, and mark which are usually negotiable with large SaaS vendors (often: breach notice timing, objection rights, clarity on data use) and which usually are not (bespoke audit rights for small customers).
7. List the questions for counsel.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Quote the DPA with clause numbers for every finding. Do not invent clauses; write "not stated" when absent.
- Name articles or legal requirements only where you are confident they apply to the stated framework, and mark interpretations as such.
- Do not declare the DPA compliant or non-compliant overall; give the gap list and say which gaps matter most for the data described.
- Calibrate to the data: special-category, children's or financial data, or large volumes, raise the stakes and the recommendation for counsel review.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## In brief
Four lines: what this DPA is, the roles, the data it was assessed against (or the assumption made), the three biggest gaps.

## Requirement check
Table: requirement | status | clause (quoted) | why.

## Other risk points
Table: topic | what the DPA says | risk | ask.

## Missing annexes
Bullets, or "None".

## Ask the vendor
Numbered by risk: ask - proposed wording or fallback - usually negotiable?

## To verify with counsel
Numbered questions.
</output_format>
