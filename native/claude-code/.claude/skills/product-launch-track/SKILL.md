---
name: product-launch-track
description: Takes a launch from positioning to a tiered plan, launch assets, a go or no-go readiness review and a post-launch retro, pausing for approval between steps.
license: CC0-1.0
arguments:
  - feature
argument-hint: <feature>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: product-launch
  source: https://hermes-ide.com/prompts/product-launch-track
  catalog: 2026.1003.0
---

# Product launch track

## Inputs

- `feature` (required): What is launching, who it is for, the problem it solves, pricing and availability, status, and the target launch date if known.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs the launch of the following feature, one approved step at a time:

<feature>
$feature
</feature>

First the positioning (who it is for, the problem, the alternatives and the message), then a launch plan sized to the right tier, then the assets (announcement, enablement, help and support content), then a go or no-go readiness review just before launch, and finally a retro once results are in. Each step produces one document and stops for the owner's approval or edits; later steps build on the approved versions instead of re-asking. The assistant never invents facts, metrics, quotes, owners or dates: anything missing becomes a clearly marked placeholder or a question. The launch owner makes every go, no-go and messaging decision.

## Steps

Work through these steps in order. Do not skip a gate.

1. positioning (plan)
2. plan (plan)
3. assets (build)
4. readiness (verify)
5. retro (review)

### Step 1: Positioning

Establish what this launch is and what it should say before anything is planned or written.

1. Ask the owner, in one message, for anything essential that is missing: the target customer and buyer, the problem and how people solve it today, pricing and plan availability, the current status (beta results, feature flags), the launch date or window, and any proof (beta metrics, customer quotes). If enough is already given, skip the questions.
2. When you have the answers, write:
   - **Target customer:** who it is for, the trigger situation that makes them need it, and who it is not for.
   - **Problem and alternatives:** the problem in the customer's words and what they use today, including doing nothing.
   - **What is different:** two or three capabilities that matter against those alternatives, each with its proof or marked [NEEDS PROOF].
   - **Positioning statement:** For [target customer] who [need], [feature] is a [category] that [key benefit]. Unlike [alternative], it [main difference].
   - **Message hierarchy:** one headline message and three supporting messages, each with its proof point.
   - **Recommended launch tier:** major, minor or silent, with the reason in two sentences.
3. Flag any claim that cannot be backed with the evidence given.

Stop and wait for approval or edits. Do not start the plan.

**Gate:** stop here and wait for the user's approval before step 2 (plan).

### Step 2: Launch plan

Build the launch plan for the approved positioning and tier.

1. Write a readiness checklist by function, scaled to the tier: product and engineering (feature flags, monitoring, staged rollout), quality, security and privacy, legal (terms, claims), support (training, macros, escalation), documentation, sales and customer success, marketing, analytics (events and dashboards live before launch), billing and operations. A silent launch needs only flags, monitoring, docs, a changelog entry and a support heads-up.
2. Give every item an owner as a role placeholder ([PM], [Support lead]) and a due date relative to launch (T-14, T-7 and so on), or calendar dates if the launch date is known. Flag weekends, likely holidays and Friday launches.
3. Write the communications timeline: internal announcement, enablement, asset freeze, go or no-go meeting, rollout stages, external messages by channel, launch-day monitoring, and check-ins at T+7 and T+30.
4. Define go or no-go criteria now, before anyone is attached to the date.
5. Write the rollback plan: triggers, who decides, how to roll back, and how to tell customers.
6. Set success metrics: adoption, the outcome the feature should move, and guardrails, each with a target labelled as a proposal if not given, a window and a review date.

Present the plan as tables. Stop and wait for approval or edits. Do not write assets yet.

**Gate:** stop here and wait for the user's approval before step 3 (assets).

### Step 3: Launch assets

Write the assets the approved plan calls for, all built on the approved message hierarchy.

1. List the assets the tier needs and confirm the list with the plan: for example a blog post, a customer email, an in-app message, a changelog entry, a sales and customer success enablement brief, a help article and support macros. A silent launch needs only the changelog entry, the help article update and a support note.
2. Write each asset:
   - Customer-facing pieces lead with the reader's problem, show how to get started in a few steps, and state availability and limits exactly. No "excited to announce", no hype words, no invented quotes or metrics; use [IMAGE], [QUOTE NEEDED] and [CONFIRM] placeholders.
   - The enablement brief is internal and scannable: one-line description, who it is for and not for, a 30-second talk track, discovery questions, an objections table, what not to promise, availability and pricing, and an FAQ.
   - Support content covers the top questions and known limits, with the escalation path.
3. Check every asset against the positioning: same headline message, same availability, no claim beyond the proof. List any inconsistencies you fixed.

Stop and wait for approval or edits to each asset. Do not run the readiness review yet.

**Gate:** stop here and wait for the user's approval before step 4 (readiness).

### Step 4: Readiness review

Run the go or no-go review shortly before launch.

1. Ask the owner for the current status of every readiness item and go or no-go criterion from the approved plan: done, at risk or not done, with a note. Also ask about open bugs by severity, monitoring and alerting, support training, docs, legal sign-off and anything that changed since the plan was approved. Do not mark anything as done on your own.
2. When you have the status, produce:
   - **Status table:** item, owner, status, note, and whether it blocks launch.
   - **Recommendation:** go, go with conditions (list each condition and its owner and deadline), or no-go (what must happen first and a proposed new date or decision point).
   - **Launch-day runbook:** the order of steps, who watches which dashboards, the rollback triggers from the plan, and when and how the team will check in.
3. Be direct. If a blocking criterion is not met, recommend no-go or a conditional go even if the date is fixed, and say what the risk is.

Stop and wait for the owner's go or no-go decision. Run the retro only after the launch, once results are in.

**Gate:** stop here and wait for the user's approval before step 5 (retro).

### Step 5: Retro

Review the launch once enough time has passed to read the success metrics, usually 2 to 6 weeks after launch.

1. Ask for the results against each success metric from the plan, with the comparison used (holdout, test or before-and-after), adoption numbers, support volume and themes, incidents, and qualitative feedback.
2. Write the results review:
   - **Scorecard:** metric, target, actual, met, missed or unclear. Judge against the targets agreed in the plan; do not swap in metrics that happened to rise.
   - **Signal or noise:** for each key result, whether the comparison, sample size, time window and novelty effects make it trustworthy.
   - **Recommendation:** scale, iterate, hold for more data, or roll back, with the deciding reasons.
3. Write the process retro: what went well, what went badly, and what to change for the next launch, covering positioning, planning, assets, readiness and communication. Each change gets an owner role.
4. List the follow-ups: product changes, content updates and the next review date.

This is the last step.
