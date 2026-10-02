---
name: write-runbook
description: Writes a runbook for an alert or routine procedure with symptoms, diagnosis commands, ordered mitigations, verification and escalation. Use so on-call engineers can act without tribal knowledge.
license: CC0-1.0
arguments:
  - alert_or_procedure
  - system_context
argument-hint: <alert_or_procedure> [system_context]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: incident
  source: https://hermes-ide.com/prompts/write-runbook
  catalog: 2026.1002.0
---

# Write an operational runbook

## Inputs

- `alert_or_procedure` (required): The alert (name, condition, query, threshold) or the routine procedure to document, e.g. "rotate the TLS certificate on the public load balancer".
- `system_context` (optional): Architecture, dashboards, log locations, tooling, owners and known past causes.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A runbook is read by a tired engineer who may never have touched this system, often in the middle of the night. It must get them from "an alert fired" to "impact reduced" with commands they can paste, and it must tell them when to stop and call someone. Runbooks fail when they explain architecture at length, give commands with no expected output, or put a risky fix before a safe one.
</context>

<task>
Write a runbook for:
$alert_or_procedure
Only if system_context was provided: 
System context:
$system_context

1. Decide which kind this is. For an alert, write the alert flow below. For a routine procedure, replace Triage, Diagnosis and Mitigations with Preconditions, Steps (each with a checkpoint) and Rollback.
2. Summary: what the alert means in user terms, likely user impact, severity guidance, and the most common known causes if given.
3. Triage (first 5 minutes): how to confirm the alert is real, how to size the impact, and whether to escalate immediately.
4. Diagnosis: read-only checks in order of likelihood. Each check gives the command or query, what a healthy result looks like, and what an unhealthy result means and which mitigation it points to.
5. Mitigations: ordered from safest and most reversible to riskiest. Each states when to use it, the exact steps, the risk, and how to undo it.
6. Verification: the signals that prove the mitigation worked and how long to watch them.
7. Escalation: when to escalate, to whom (role or team), and what information to hand over.
</task>

<constraints>
- Never invent hostnames, dashboard links, metric names, namespaces or team names. Use placeholders in angle brackets such as `<service-namespace>` and list every one under "Fill before publishing".
- Put every command in a fenced block. Mark any command that changes state with "CHANGES STATE" and any that can lose data or drop traffic with "DESTRUCTIVE", and require a check before running it.
- Keep it scannable: numbered steps, short sentences, no history lessons.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Summary
## Triage
## Diagnosis
## Mitigations
## Verification
## Escalation
## Fill before publishing
A checklist of every placeholder and unconfirmed assumption.
</output_format>
