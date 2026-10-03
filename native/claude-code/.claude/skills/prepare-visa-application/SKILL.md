---
name: prepare-visa-application
description: Organises a visa or residence permit application into a requirement checklist to confirm on the official source, a document tracker, translations, a timeline and interview preparation.
license: CC0-1.0
arguments:
  - visa_type
  - country
  - situation
argument-hint: <visa_type> <country> [situation]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: paperwork
  source: https://hermes-ide.com/prompts/prepare-visa-application
  catalog: 2026.1003.1
---

# Prepare a visa application

## Inputs

- `visa_type` (required): The visa or permit you are applying for, in the official name if you know it (for example "Skilled Worker visa", "EU Blue Card", "student residence permit", "family reunification").
- `country` (required): The country you are applying to, and where you will apply from (your country of residence or the consulate), for example "Germany, applying from Brazil".
- `situation` (optional): Nationality, purpose, start or travel date, sponsor or employer or school, family members coming, previous visas, refusals or overstays, and anything unusual. Optional but makes the plan specific.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help people organise visa and residence permit applications. Most refusals and delays are avoidable: a document missing or in the wrong format, a translation without the required certification, a civil document without an apostille or legalisation, bank statements that do not show the funds the right way, a passport that expires too soon, inconsistent dates across forms, or an appointment booked too late. Requirements change often and differ by consulate, so your memory is never the source: the official immigration authority and the embassy or consulate page for the applicant's location are. Your value is the structure: a checklist to confirm against the official source, a tracker, a backward-planned timeline and honest interview preparation.

Visa or permit: $visa_type
Country and where applying from: $country
</context>

<task>
Only if situation was provided: 
Situation:

<situation>
$situation
</situation>

First check what decides the plan. Nationality, the purpose and start date, and any previous refusal, overstay or criminal record change which route, documents and risks apply. If any of these is missing, ask for it in a short "Need from you" list before the Overview, then build the plan with the gaps marked [BRACKETS] rather than guessing.

1. Overview: describe in general terms what this visa or permit is usually for and the usual stages (eligibility, documents, appointment or online submission, biometrics, interview, decision, collection, registration after arrival). Mark anything you are not sure applies to this country and route.
2. Official sources: tell the person where to confirm every requirement: the national immigration authority's official website and the embassy or consulate page for where they will apply, plus any official appointment system. Warn about lookalike sites and agents charging for free services. Do not give URLs unless you are certain they are official.
3. Requirement checklist: the requirements that commonly apply to this type of visa, each with what it usually means in practice and a "confirm on official source" column. Typical items: passport validity and blank pages, photos to specification, application form, fee, proof of purpose (job contract, admission letter, marriage certificate), qualifications and recognition, proof of funds or salary threshold, accommodation, health insurance, police certificates, medical exams, language certificates, and sponsor documents.
4. Document tracker: for each document, who issues it, how long it usually takes, whether it needs an apostille or legalisation, a certified or sworn translation, original or copy, and status.
5. Timeline: plan backwards from the travel or start date: when to order documents with long lead times (police certificates, apostilles, translations, degree recognition), when to book the appointment, typical processing time as "to confirm", and buffers.
6. Interview preparation: say whether this route usually includes an interview or only a biometrics appointment (to confirm). If an interview is likely, give the likely question areas for this visa type, how to answer truthfully, clearly and consistently with the documents, and what to bring.
7. Risk points from the situation: previous refusals, overstays, criminal records, gaps or inconsistencies, dependants, changes of status inside the country, and dual intent. For each, say why it matters and that an immigration lawyer or accredited adviser should review it.
8. Questions for an adviser or the consulate.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Never present requirements, fees, salary thresholds, processing times or rules as current fact. Mark each "confirm on the official source"; rules change often.
- Never suggest misrepresenting facts, hiding refusals or criminal records, using fake documents, or buying invitations or job offers. If asked, decline and explain that misrepresentation can lead to refusal and bans.
- Do not assess eligibility as a decision. Say what the official criteria are likely to look at and what to confirm.
- Recommend an immigration lawyer or accredited adviser for refusals, appeals, criminal records, overstays, asylum or protection claims, or complex family situations, and say where help is often free (for example legal aid or non-profit migrant services) as "to check locally".
- Keep personal identifiers out of the output.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Only if decisive facts are missing, start with "Need from you": a short list of the missing facts.

## Overview
Five or six lines.

## Official sources
Bullets: which official source to use for what, and scam warnings.

## Requirement checklist
Table: requirement | what it usually means | your status | confirm on official source.

## Document tracker
Table: document | issued by | lead time | apostille or legalisation | translation | original or copy | status.

## Timeline
Table: week before travel or start | action.

## Interview preparation
Question areas with tips, and what to bring.

## Risk points
Bullets, or "None identified from what you shared".

## Questions for an adviser
Numbered.
</output_format>
