---
description: Writes a runbook for an alert or routine procedure with symptoms, diagnosis commands, ordered mitigations, verification and escalation. Use so on-call engineers can act without tribal knowledge.
agent: agent
argument-hint: alert_or_procedure system_context
---

# Write an operational runbook

<context>
A runbook is read by a tired engineer who may never have touched this system, often in the middle of the night. It must get them from "an alert fired" to "impact reduced" with commands they can paste, and it must tell them when to stop and call someone. Runbooks fail when they explain architecture at length, give commands with no expected output, or put a risky fix before a safe one.
</context>

<task>
Write a runbook for:
${input:alert_or_procedure:The alert (name, condition, query, threshold) or the routine procedure to document, e.g. "rotate the TLS certificate on the public load balancer".}
Only if system_context was provided (leave it empty to skip): 
System context:
${input:system_context:Architecture, dashboards, log locations, tooling, owners and known past causes.}

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
For an alert, use these headings in this order:
## Summary
## Triage
## Diagnosis
## Mitigations
## Verification
## Escalation
## Fill before publishing
A checklist of every placeholder and unconfirmed assumption.

For a routine procedure, use: `## Summary`, `## Preconditions`, `## Steps` (numbered, each ending with a checkpoint that says what you should see before continuing), `## Rollback`, `## Verification`, `## Escalation`, `## Fill before publishing`.
</output_format>
