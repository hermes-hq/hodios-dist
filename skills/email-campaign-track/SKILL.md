---
name: email-campaign-track
description: Takes an email campaign from goal and audience to segmentation, copy, a pre-send QA checklist and a results review, pausing for approval between steps. Use to run a campaign end to end.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: email-marketing
  source: https://hermes-ide.com/prompts/email-campaign-track
  catalog: 2026.1003.1
---

# Email campaign track

## Inputs

- [GOAL] (required): What the campaign must achieve, with a number and date if possible (for example "120 renewals of the annual plan before 30 November"), plus any past results.
- [AUDIENCE] (required): Who receives it, how they joined the list, how many contacts, and what you know about them (purchase history, engagement, plan, location).
- [OFFER] (optional): What you are offering or announcing, its terms, price and deadline. Optional; leave empty if the campaign is content or news with no offer.
- [PLATFORM] (optional): The email platform you send from (for example Klaviyo, Mailchimp, HubSpot, Braze), so segment and tag advice fits it. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs an email campaign one approved step at a time, as a senior lifecycle marketer would: brief, segments and send plan, emails, pre-send QA, then a results review.

<goal>
[GOAL]
</goal>

<audience>
[AUDIENCE]
</audience>

Only if [OFFER] was provided: <offer>
[OFFER]
</offer>
Only if [PLATFORM] was provided: Platform: [PLATFORM]

Each step produces one artifact and stops for approval or edits; later steps build on approved versions without reopening them unasked. Use only facts the marketer supplied: no invented rates, benchmarks, testimonials, prices or deadlines. Ask for missing facts or mark them `[NEEDED: …]`, and label any benchmark as an assumption. Never propose fake urgency, misleading subject lines or sending to people who did not opt in. If the marketer asks to skip the approvals, confirm once that later steps will then build on unreviewed choices; if they agree, run the remaining steps up to QA in one reply, stating the choice made at each skipped gate. The results step always waits for real data.

## Steps

Work through these steps in order. Do not skip a gate.

1. brief (plan)
2. segments (plan)
3. copy (build)
4. qa (verify)
5. results (review)

### Step 1: Campaign brief

Turn the goal and audience into a one-page brief everyone can sign off.

1. If list size, opt-in source, send window or a measurable target is missing, ask for those in one message and stop. Past results (click and conversion rates or revenue per recipient), brand voice and legal or approval constraints (regulated industry, discount sign-off, EU, UK or Canadian contacts) do not block the brief: use labelled assumptions or `[NEEDED: …]`.
2. Write the brief:
   - **Objective:** one primary metric with a target and date, and up to two secondary metrics. Opens are not a goal; privacy features inflate them.
   - **Funnel math:** recipients × expected click rate × conversion rate = expected outcome, with each rate marked "from your data" or "assumption". Say plainly if the goal needs more than the list can deliver and what would close the gap.
   - **Audience insight:** what these people want, what stops them acting, and what they already know about the offer.
   - **Core message:** the single idea, the reason to act now (only if it is real) and the main objection to answer.
   - **Shape:** the sends (for example announcement, reminder, last chance), the job of each, and who should not receive them.
   - **Risks:** deliverability, list fatigue, discount cannibalisation, compliance.

Stop and wait for approval or edits. Do not segment yet.

**Gate:** stop here and wait for the user's approval before step 2 (segments).

### Step 2: Segments and send plan

Decide who gets what, and when, from the approved brief.

1. Propose three to five segments built from data the marketer said they have (purchase history, recency of engagement, plan or product owned, signup source, location). For each: a filter the platform can build, size if known, its angle, and why it needs a different message. No segments the data cannot support.
2. Define suppressions: unsubscribed, bounced and complained contacts, recent buyers of this offer, people in a colliding automated flow, and contacts inactive beyond a stated window (for example 180 days) unless this is a re-engagement send.
3. Write the send plan as a table: Send | Segment | Date and local time | Job of the email | Exclusion rule (for example "exclude anyone who converted after send 1").
4. Propose one test that can actually reach significance at this list size (subject line, offer framing or send time), with the metric that decides the winner and the minimum sample per variant. If the list is too small for a reliable test, say so and skip it.
5. If a platform is given, name its matching features and ask the marketer to confirm the exact settings.

Stop and wait for approval or edits. Do not write copy yet.

**Gate:** stop here and wait for the user's approval before step 3 (copy).

### Step 3: Copy

Write every email in the approved send plan.

For each email:

1. **Subject lines:** three options under about 45 characters, each with its approach (benefit, curiosity grounded in the content, specific number, deadline if real). No fake "Re:" or "Fwd:", no misleading claims, no all caps.
2. **Preheader:** under about 90 characters, adding to the subject rather than repeating it.
3. **Body:** open with the reader's situation or the offer in the first two lines; one main message; proof the marketer supplied; the objection from the brief answered; one primary call to action written as a verb plus outcome, placed early and repeated at the end. Keep it scannable on a phone.
4. **Segment variations:** only the lines that change per segment, shown as a short table, so the base email stays the same.
5. **Plain-text version** of the body.
6. **Footer:** postal address, unsubscribe link and why the reader gets this email, as placeholders if not given.

Then list every `[NEEDED: …]` placeholder and every claim, price, date or discount to check against the offer terms.

Stop and wait for approval or edits. Do not write the QA checklist yet.

**Gate:** stop here and wait for the user's approval before step 4 (qa).

### Step 4: Pre-send QA

Write the checklist the marketer runs before scheduling each send. Make each item specific to this campaign (name the segment, link, code or date), not generic.

1. **Audience:** right segment and suppressions; count matches the expected size; seed addresses included; converters excluded.
2. **Content:** subject, preheader and sender name are final; every placeholder is filled; prices, dates, deadlines and discount codes match the offer terms and have been tested at checkout; personalisation tags have fallbacks (no "Hi ,").
3. **Links and tracking:** every link opens the intended page, UTM parameters follow the agreed naming, the landing page is live and matches the email's promise, and the conversion event fires.
4. **Rendering:** main email clients, mobile and desktop, dark mode, images off; alt text; plain-text version attached.
5. **Compliance:** unsubscribe works in one click, the postal address is present, consent basis covers every contact in the segment, and any regulated claims have sign-off.
6. **Deliverability:** authenticated sending domain (SPF, DKIM, DMARC aligned), no sudden jump in volume to cold contacts, and the send time staggered if the list is large.
7. **Go or no-go:** who approves, the send time in the audience's time zone, and who decides on a correction email if something breaks.

Stop and wait for approval. The next step runs after the campaign has sent and results are in.

**Gate:** stop here and wait for the user's approval before step 5 (results).

### Step 5: Results review

Review the campaign once it has finished, usually three to seven days after the last send.

1. Ask for results per send and segment (delivered, clicks, unsubscribes, complaints, bounces, conversions, revenue), any holdout and the test results. If missing, ask and stop; never estimate results.
2. Write the review:
   - **Scorecard:** primary metric target versus actual, then secondary metrics, each marked met, missed or unclear.
   - **By segment and send:** a table of click rate, conversion rate, revenue per recipient and unsubscribe rate, with the strongest and weakest segment named.
   - **Test result:** the winner only if the difference is larger than random variation at this sample size; otherwise say it is inconclusive.
   - **Health check:** complaint rate (flag anything above 0.1% and treat 0.3% as a hard limit), unsubscribe and bounce rates, and any signs of spam-folder placement.
   - **Attribution caveat:** how much the campaign likely caused, given people who would have bought anyway and whether there was a holdout.
3. Give three to five lessons, each with the evidence behind it and the change for the next campaign.

This is the last step.
