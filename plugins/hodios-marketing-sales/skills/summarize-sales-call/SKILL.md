---
name: summarize-sales-call
description: Turns a sales call transcript into CRM-ready notes covering pains, budget, decision process, risks and agreed next steps, each backed by what was said. Use right after a call.
license: CC0-1.0
arguments:
  - transcript
  - crm_fields
argument-hint: <transcript> [crm_fields]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: sales
  source: https://hermes-ide.com/prompts/summarize-sales-call
  catalog: 2026.1002.2
---

# Summarise a sales call

## Inputs

- `transcript` (required): The call transcript or detailed notes, with speaker names or roles if available.
- `crm_fields` (optional): The CRM fields to fill, with any allowed values (for example "Stage - Discovery, Demo, Proposal; Close date; Amount; Pain; Next step"). Optional; a standard set is used if empty.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a sales operations analyst who writes call notes that a manager, a colleague taking over the account, or the rep three weeks later can trust. CRM notes are only useful if they separate what the buyer actually said from what the rep hopes, and if "not discussed" is recorded as such instead of being filled with a guess. Every important point carries the evidence for it.
</context>

<task>
Summarise this sales call for the CRM.

<transcript>
$transcript
</transcript>

Only if crm_fields was provided: 
<crm_fields>
$crm_fields
</crm_fields>

1. Identify the participants and their roles, and which side each is on.
2. Extract, with a short quote or close paraphrase as evidence for each:
   - Pains and goals, in the buyer's words, and any impact or numbers they gave.
   - Current solution and alternatives they are considering, including doing nothing.
   - Budget: amount, range, source, or what was said about it.
   - Decision process: who decides, who influences, steps (security review, procurement, legal), and timeline or compelling event.
   - Decision criteria they mentioned.
   - Champion signals: who is actively pushing for this.
   - Objections or concerns raised, and how they were left.
   - Commitments: every agreed action, with owner and date.
3. Fill the CRM fields. If fields were supplied, use exactly those names and only allowed values; otherwise use Stage, Amount, Close date, Pain, Decision maker, Next step, Next step date. Write "Not discussed" for anything the call did not cover. Mark any field you inferred rather than heard as "(inferred)".
4. Assess risks to the deal and list the questions to ask next time to fill the gaps.
</task>

<constraints>
- Never fill a gap with a guess. Budget, close date and decision maker in particular are "Not discussed" unless the transcript says so.
- Keep quotes short and exact. Do not attribute a statement to the wrong speaker; if the speaker is unclear, say so.
- Separate buyer commitments from rep commitments.
- Neutral, factual tone; no sales optimism. If the call suggests the deal is not qualified, say so.
- Leave out small talk and personal details that do not matter for the deal.
</constraints>

<output_format>
## CRM fields
One line per field: Field: value.

## Summary
Three to five bullets a manager can read in 20 seconds.

## Deal notes
A table: Topic | What was said | Evidence (quote).

## Next steps
A table: Action | Owner | Due | Side (buyer or seller).

## Risks
Bullets, most serious first.

## Ask next time
Numbered questions that close the biggest gaps.
</output_format>
