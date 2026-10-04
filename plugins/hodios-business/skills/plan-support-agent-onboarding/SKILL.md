---
name: plan-support-agent-onboarding
description: Plans a new support agent's first weeks - product learning, tools and access, shadowing, graduated queues, quality checks, and readiness criteria for each stage - week by week.
license: CC0-1.0
arguments:
  - team
  - weeks
argument-hint: <team> [weeks]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: customer-support
  source: https://hermes-ide.com/prompts/plan-support-agent-onboarding
  catalog: 2026.1004.3
---

# Plan onboarding for a new support agent

## Inputs

- `team` (required): The support team and product - what customers contact you about, channels (email, chat, phone), tools (help desk, CRM, knowledge base), team size, who will train and buddy the new agent, and the new agent's experience.
- `weeks` (optional; default: 4): Length of the onboarding plan in weeks.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a support team lead who has onboarded many agents. New agents fail in predictable ways: they get a week of reading and then the full queue, they learn the tools but not the product, nobody reviews their first replies, and they quietly guess at policy. A good ramp moves from learning to watching to doing with a safety net: shadowing, then simple ticket types with every reply reviewed, then more complex ones as quality holds, with clear criteria to move up. It protects customers from beginner mistakes and the new agent from being thrown in.
</context>

<task>
Plan a $weeks-week onboarding for a new support agent.

<team>
$team
</team>

1. Before day one: accounts and tool access to request, equipment, a buddy assigned, a welcome message, and the reading list (top help articles, tone guide, policies).
2. Ramp overview: the stages (learn, shadow, reverse-shadow, supervised queue, independent) spread across $weeks weeks, with what the agent can and cannot do at each stage.
3. Week-by-week plan: daily focus for week one (product as a customer would use it, tools, the top ten contact reasons, policy and escalation paths, shadowing a few hours a day) and weekly goals afterwards. Include hands-on product practice and a short daily check-in.
4. Graduated queues: order ticket types from simple to complex based on the contact reasons given (for example "where is my order" before billing disputes before technical bugs), by channel (email before chat before phone, unless the team works differently), with volume targets that build gradually.
5. Quality checks: every reply reviewed before sending in the first stage, then a sample, using the team's quality scorecard if it has one (otherwise a simple five-point check: accuracy, completeness, tone, policy, next step), with feedback given the same day.
6. Readiness criteria: measurable conditions to move from one stage to the next and to finish onboarding, such as a quality score over several consecutive reviews, handling each ticket type correctly, and knowing when to escalate. Avoid speed targets before quality is consistent.
7. Buddy and manager guide: what the buddy does daily, the manager's weekly one-to-ones, the questions to ask, and warning signs that the ramp needs adjusting.
</task>

<constraints>
- Fit the plan to the team size and channels given. If the team has no trainer, design it for a buddy who also handles their own queue.
- Do not invent product details, policies or tool features; refer to them by the names given and mark anything missing as `[ADD: …]`.
- If $weeks is too short for the product's complexity, say so and show what to cut or extend.
- Volume targets are starting suggestions, labelled as such, to be tuned with the team's own data.
</constraints>

<output_format>
## Before day one
Checklist.
## Ramp overview
Table: Stage | Weeks | Can do | Cannot do yet.
## Week-by-week plan
Week one by day, then each later week with goals and activities.
## Graduated queues
Table: Order | Ticket type or channel | Start week | Review level | Starting volume.
## Quality checks
## Readiness criteria
Table: Gate | Criteria | Who signs off.
## Buddy and manager guide
## Questions
At most three.
</output_format>
