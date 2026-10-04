---
name: customer-feedback-loop-track
description: Runs a recurring customer feedback loop in approved steps, collecting from every channel, tagging, finding themes, prioritising with the team, deciding and closing the loop with customers.
license: CC0-1.0
arguments:
  - channels
  - team
  - cadence
argument-hint: <channels> <team> [cadence]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: user-feedback
  source: https://hermes-ide.com/prompts/customer-feedback-loop-track
  catalog: 2026.1004.3
---

# Customer feedback loop track

## Inputs

- `channels` (required): Where feedback arrives (support tickets, sales notes, surveys, reviews, community, interviews) and roughly how much per channel per cycle.
- `team` (required): Who takes part in prioritising and deciding (for example "PM, design lead, eng lead, head of support"), and who owns customer replies.
- `cadence` (optional; one of: monthly, quarterly; default: monthly): How often the loop runs.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs one $cadence cycle of the customer feedback loop for this team, one approved step at a time.

<channels>
$channels
</channels>

<team>
$team
</team>

The cycle collects feedback from every channel, tags it with a consistent scheme, synthesises themes with counts and quotes, prepares and runs a prioritisation session with the team, records decisions with owners, and closes the loop with the customers who gave the feedback. Each step produces one artifact and waits for approval; later steps build on the approved versions. The assistant works only from feedback the user pastes or summarises, never invents quotes, counts or customers, and removes personal data from anything meant for a wider audience. Decisions belong to the team: the assistant prepares evidence and options, and records what the team decides. If the user wants to skip the gates, confirm once that later steps will build on unreviewed tagging and themes; if they agree, run the remaining steps in one reply and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. collect (discover)
2. tag (discover)
3. synthesise (review)
4. prioritise (plan)
5. decide (plan)
6. close-loop (ship)

### Step 1: Collect

Gather this cycle's feedback from every channel.

1. Ask the user to paste or summarise the feedback for this cycle from each channel listed, with source, date, customer segment or plan, and revenue where known. Ask also for last cycle's decisions, so this cycle can check whether shipped changes moved anything. Wait for the material.
2. When it arrives, build a coverage table: channel, number of items, date range, and which segments are represented. Point out channels that are silent this cycle and segments that are missing or over-represented (for example only enterprise accounts in sales notes).
3. Remove duplicates (the same customer raising the same issue in two channels counts once, with both sources noted) and strip personal data such as emails and phone numbers.
4. Flag anything urgent that should not wait for the cycle: security or privacy reports, data loss, outages, or a customer at immediate risk of leaving. Recommend routing those now.

Stop and wait for the user to confirm the collected set is complete enough. Do not tag yet.

**Gate:** stop here and wait for the user's approval before step 2 (tag).

### Step 2: Tag

Tag every item in the approved set.

1. Ask whether the team has a tagging scheme. If it does, ask for it and use it exactly. If not, propose a minimal one: feedback type (bug, feature request, usability, performance, pricing, praise, churn reason, other) and product area (from the areas the user names), with one-line definitions.
2. Tag each item with one type and one area. Split items that raise several issues into separate rows.
3. Record the tricky calls: items where two tags were plausible, and the rule you used, so the team can keep tagging consistent.
4. Report the "other" share; if it is above about 10 percent, suggest the new tag the uncategorised items point to.

Present the tagged table (item summary, type, area, source, segment) and the tricky calls. Stop and wait for the user to correct tags or approve.

**Gate:** stop here and wait for the user's approval before step 3 (synthesise).

### Step 3: Synthesise

Turn the approved tags into themes the team can act on.

1. Group tagged items into themes: a theme is a shared underlying problem, not just a shared tag ("can't see who changed a booking" and "need an audit log" may be one theme).
2. For each theme: a one-sentence problem statement in the customer's terms, the number of distinct customers, the channels and segments it appears in, revenue involved if known, two short verbatim quotes, and the trend against last cycle if known.
3. Check last cycle's shipped changes: does this cycle's feedback show the problem shrinking, unchanged or shifting?
4. Note what the data cannot show: silent segments, channels that over-represent loud customers, and small counts that could be noise.
5. Rank themes by breadth (customers affected) and severity (blocks work, costs money, or annoys), and show both, not a single blended score.

Present the theme report. Stop and wait for the user to approve it before the team session is prepared.

**Gate:** stop here and wait for the user's approval before step 4 (prioritise).

### Step 4: Prioritise with the team

Prepare and support the prioritisation session with the team listed.

1. Write a one-page pre-read: the top themes (at most seven) from the approved report, each with the evidence, the customer quote, and what is already planned that touches it. Send-ready in plain language.
2. Propose a 45-to-60-minute agenda: five minutes on what changed since last cycle, theme review with questions from each function, a vote or scoring round, and decisions. Suggest a simple, transparent method the team can use, such as impact versus effort with each function estimating its own part, and remind them that effort estimates belong to the people doing the work.
3. Give each theme the questions a good session would ask: is this the real problem? which customers matter most here? is there a cheaper way to test a fix? what happens if we do nothing for a cycle?
4. After the session, ask the user for the outcome: the scores or votes, and the discussion points.

Stop after presenting the pre-read and agenda, and wait for the user to bring back the session outcome.

**Gate:** stop here and wait for the user's approval before step 5 (decide).

### Step 5: Decide

Record the team's decisions from the session outcome.

1. For each theme discussed, record one decision: build now, explore (discovery or a small test), fix as a bug, address with content or support (documentation, onboarding, a help article), park with a review date, or decline.
2. For each decision: the owner, the next action and its date, how the team will know it worked (the signal to watch next cycle), and the customer message it allows (what can honestly be said now).
3. For declined or parked themes, write the reason in a sentence customers would accept.
4. Point out any decision without an owner or date, and any theme the session ran out of time for.

Present the decision log. Stop and wait for the user to confirm it is accurate before customer messages are drafted.

**Gate:** stop here and wait for the user's approval before step 6 (close-loop).

### Step 6: Close the loop

Tell customers what happened to their feedback.

1. Group the customers who gave feedback by decision: shipped or fixed, building, exploring, parked, declined.
2. Draft one short message template per group, personalisable by name and their specific issue: thank them, say what was decided and why, what they can do now (a workaround, how to use the fix, an invitation to a research session), and when they will hear more. Never promise dates the decision log does not contain.
3. Draft a short internal update for support and sales: what was decided, what they may now tell customers, and what they must not promise.
4. If the team publishes a changelog or public roadmap, suggest the one or two lines it could add.
5. List the signals to check at the start of the next $cadence cycle, taken from the decision log.

Present the messages and the internal update. This is the final step of the cycle.
