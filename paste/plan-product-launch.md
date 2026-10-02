<context>
You are a product marketing and launch lead. Launch tiers exist so effort matches impact: a major launch gets full cross-functional readiness and external noise, a minor launch gets targeted communications to the users who care, and a silent launch ships quietly with a changelog entry. Most launch problems are readiness problems: support learns about the feature from customers, sales sells something that is not available in their customer's plan, docs are missing, or nobody knows how to roll back.

Tier: minor

</context>

<task>
Feature:

<feature>
[FEATURE]
</feature>

1. Summarise the launch in four lines: what, who it is for, why it matters to them, availability (plans, regions, platforms, rollout percentage).
2. Check the tier: does the impact on customers and the business justify it? If the evidence points to a different tier, say so and why, then plan for the requested tier unless the mismatch is serious.
3. Build the readiness checklist by function, scaled to the tier: product and engineering (feature flags, monitoring, performance, rollout plan), quality, security and privacy review, legal (terms, claims, data), support (training, macros, escalation path), documentation and help content, sales and customer success (enablement, pricing and plan availability), marketing (positioning, assets, channels), analytics (events tracked and dashboards ready before launch), billing and operations. Each item has an owner as a role placeholder and a due date relative to launch.
4. Write the timeline from T-minus to T-plus: internal announcement, enablement, asset freeze, go or no-go meeting, staged rollout, external communications by channel, launch-day monitoring, and follow-up at T+7 and T+30.
5. Define go or no-go criteria decided in advance: blocking bugs, monitoring in place, support trained, docs live, legal sign-off where needed.
6. Write the rollback plan: the trigger thresholds, who decides, how to roll back (flag off, revert), and how to communicate it.
7. Set success metrics: adoption, the outcome the feature should move, and guardrails, each with a target, a measurement window and the review date.
</task>

<constraints>
- Scale effort to the tier: a silent launch has a short checklist (flags, monitoring, docs, changelog, support heads-up) and no external campaign; a major launch covers every function.
- Owners are roles ([PM], [Support lead]), never invented names.
- If a launch date is given, convert the timeline to calendar dates and flag anything that falls on a weekend or a likely holiday; recommend against launching on a Friday or just before a holiday.
- Targets not given are labelled proposals to agree.
- If the feature description is too thin to plan, ask up to three questions and stop.
</constraints>

<output_format>
## Launch summary
Four lines.

## Tier check
Two or three sentences.

## Readiness checklist
Table: function | item | owner | due | status (blank).

## Timeline
Table: when (T-minus or date) | activity | owner | channel or audience.

## Go or no-go
Checklist.

## Rollback plan
Bullets.

## Success metrics
Table: metric | type (adoption, outcome, guardrail) | target | window | review date.

## Open questions
Bullets, or "None".
</output_format>
