---
name: write-resignation-letter
description: Writes a resignation letter and a plan for the conversation with your manager, covering notice, a handover offer and tone, while keeping relationships intact. Use when you have decided to leave.
license: CC0-1.0
arguments:
  - situation
  - notice_period
argument-hint: <situation> [notice_period]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: career-growth
  source: https://hermes-ide.com/prompts/write-resignation-letter
  catalog: 2026.1002.2
---

# Write a resignation letter

## Inputs

- `situation` (required): Your role, manager, why you are leaving (as much as you want to share), whether you have a signed offer, your relationship with the team, anything sensitive (a conflict, a complaint, a competitor), and your contract's notice terms if you know them.
- `notice_period` (optional): Your notice period and proposed last day (for example "4 weeks, last day 31 May"). Leave empty if unsure; you get a placeholder and a reminder to check your contract.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help people leave jobs well. A resignation letter is a formal record, not the place to air grievances: it should state the decision, the last working day and a willingness to help with the handover, and little else. The conversation with the manager matters more than the letter: the manager should hear it first, in person or on a call, before anyone else and before the letter arrives. People who leave well keep references, rehire options and a network that follows them for decades; people who leave badly rarely gain anything from it.

<situation>
$situation
</situation>
Only if notice_period was provided: Notice and last day: $notice_period
</context>

<task>
1. Before you resign: a short checklist - a signed offer and agreed start date in hand (if moving to a new job), the notice period and any garden leave, non-compete, repayment (training, relocation, sign-on) or holiday-pay clauses checked in the contract, personal files and contacts copied appropriately without taking company data, and benefits or equity events whose timing may matter (vesting dates, bonus payment dates). Frame clause questions as things to check, and suggest HR or an employment adviser if anything is unclear.
2. Conversation plan: when and how to tell the manager (privately, first, before the letter), an opening of two or three sentences that states the decision clearly, how much to say about the reason (honest but brief and forward-looking; nothing they would regret being repeated), how to answer "where are you going?" and "why?", and what to say about the handover. Include how to handle an emotional or angry reaction calmly.
3. Resignation letter: short and formal, with the date, recipient, a clear statement of resignation, the last working day based on the notice period, an offer to support the handover, an optional one-line thanks that is sincere, and a sign-off. No complaints, no detailed reasons, no new employer's name unless they want it there. Provide a warmer and a strictly neutral version.
4. Handover outline: the sections of a handover document for their role (open work and status, recurring tasks, contacts, access and accounts, where things live, risks and deadlines) and a suggested schedule across the notice period.
5. Handling a counteroffer: questions to ask themselves before considering one (did the reasons for leaving go away, or only the pay?), and a gracious way to decline.
</task>

<constraints>
- Never invent contract terms or legal requirements. Notice rules, garden leave and final pay differ by country and contract; mark the notice period as [check your contract] if not given.
- If the situation involves harassment, discrimination, unpaid wages, a whistleblowing matter or being pushed to resign, say that resigning may affect their rights, and suggest speaking to an employment lawyer, union or official advice service before resigning.
- Keep the letter under 150 words. Keep the spoken opening under 30 seconds.
- Do not include anything in the letter that could be read as a grievance or a negotiation.
</constraints>

<output_format>
## Before you resign
Checklist.
## Conversation plan
Opening lines, answers to likely questions, and how to handle reactions.
## Resignation letter
Warmer version, then neutral version.
## Handover outline
## Handling a counteroffer
</output_format>
