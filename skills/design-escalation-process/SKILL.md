---
name: design-escalation-process
description: Designs a support escalation process - tiers, severity definitions, routing, handover templates, SLAs and how engineering is engaged. Use when tickets bounce between teams or urgent issues stall.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: customer-support
  source: https://hermes-ide.com/prompts/design-escalation-process
  catalog: 2026.1003.0
---

# Design a support escalation process

## Inputs

- [TEAM_STRUCTURE] (required): Who handles support today - tiers or roles, headcount, hours and time zones, which teams sit behind support (engineering, billing, account managers, legal), and on-call arrangements.
- [TICKET_TYPES] (optional): Common ticket types and volumes, examples of issues that were escalated badly, and customer segments or contracts with special terms. Leave empty to use a generic set.
- [TOOLS] (optional): Helpdesk, chat, issue tracker and paging tools you use.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You design support operations. A good escalation process makes three things obvious to every agent at 3 a.m.: how bad this is, who owns it now, and what the customer will hear and when. Escalations usually fail through vague severity definitions, handovers that lose context so the customer repeats themselves, engineering teams that are paged for questions the docs could answer, and tickets with no single owner while they wait between teams.
</context>

<task>
Design the escalation process.

<team_structure>
[TEAM_STRUCTURE]
</team_structure>
Only if [TICKET_TYPES] was provided: 
<ticket_types>
[TICKET_TYPES]
</ticket_types>
Only if [TOOLS] was provided: 
Tools: [TOOLS]

1. Principles: three to five rules the whole process follows (for example "the customer-facing owner stays with the ticket until it is resolved", "escalate on impact, not on how loud the customer is").
2. Severity levels: four levels from critical to low, each defined by business impact and scope (number of customers, data loss or security, money, workaround available) with two concrete examples drawn from the ticket types. Include who may set or change severity.
3. Tiers and ownership: what each tier resolves, what it must try before escalating (a checklist), and the authority it has (refunds, credits, account changes). Name the single owner role at each stage.
4. Routing rules: a decision table from ticket type and severity to destination team, plus special routes for security, data protection, legal threats, billing disputes and VIP or contractual accounts.
5. Handover template: the fields an escalation must contain (customer, impact, severity, steps to reproduce, what was tried, logs or screenshots, customer expectation set, deadline), so the next tier never has to ask the customer again.
6. SLAs: first response and update frequency per severity, and internal SLAs between tiers (time to acknowledge an escalation, time to first engineering response). Fit them to the team's hours and headcount; flag any target the current staffing cannot meet.
7. Engineering engagement: when to page versus file a ticket, the on-call path for critical issues, how bugs are linked to tickets, who updates the customer while engineering works, and how engineering hands back. Include a rule for reducing noise (for example a triage rotation that reviews non-urgent escalations daily).
8. Customer communication: templates for acknowledging an escalation, regular updates, and resolution, with honest timing language.
9. Rollout and metrics: steps to introduce the process, training, and metrics (escalation rate by tier, time in each tier, reopen rate, SLA attainment, customer satisfaction on escalated tickets) with a review after the first month.
</task>

<constraints>
- Fit the process to the stated team size and hours; a five-person team does not need four tiers. Say when a simpler design is better.
- Do not promise SLAs the staffing cannot meet; show the reasoning.
- Do not invent ticket volumes or tool features. If you mention tool configuration, describe it generically (tags, views, automations) unless the tool's capability is well known, and mark it "check in your tool".
- Security incidents and personal-data breaches may carry legal notification duties; route them to the responsible owner and note that timelines should be confirmed with them.
</constraints>

<output_format>
## Principles
## Severity levels
Table: Severity | Definition | Examples | Who can set it.
## Tiers and ownership
Table: Tier | Resolves | Must try before escalating | Authority | Owner.
## Routing rules
Table: Ticket type | Severity | Route to | Notes.
## Handover template
A copyable template.
## SLAs
Table: Severity | First response | Update frequency | Internal acknowledge | Target resolution.
## Engineering engagement
## Customer communication
Three short templates.
## Rollout and metrics
</output_format>
