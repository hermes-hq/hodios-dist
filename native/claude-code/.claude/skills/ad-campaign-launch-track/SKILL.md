---
name: ad-campaign-launch-track
description: Launches a paid ad campaign in gated steps (brief, audiences, creative, tracking QA, launch settings and a seven-day review), pausing for approval between steps. Use to launch a campaign end to end.
license: CC0-1.0
arguments:
  - offer
  - platform
  - budget
argument-hint: <offer> <platform> <budget>
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: workflow
  category: advertising
  source: https://hermes-ide.com/prompts/ad-campaign-launch-track
  catalog: 2026.1004.2
---

# Ad campaign launch track

## Inputs

- `offer` (required): What you advertise, price and offer terms, who buys and why, proof you can use, the landing page, customer value and gross margin, and any past ad results.
- `platform` (required): The ad platform and countries (for example Meta in Spain and Portugal, Google Search in the US, TikTok in the UK, LinkedIn in DACH).
- `budget` (required): The budget and period (for example "4,500 EUR for the first month"), plus any target cost per acquisition or ROAS.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Launches a paid ad campaign one approved step at a time, as a senior paid media specialist would: campaign brief with the economics, audiences, creative, tracking QA, launch settings, then a review after seven days of real data.

<offer>
$offer
</offer>

Platform: $platform
Budget: $budget

Each step produces one artifact and stops for approval or edits; later steps build on approved versions without reopening them unasked. Use only facts the marketer supplied: label benchmarks, conversion rates and cost estimates as assumptions, and mark missing facts `[NEEDED: …]`. The marketer makes every change in the ad account; you recommend settings and never claim anything was launched or changed. Never propose unsupported claims, fake urgency, personal-attribute wording, discriminatory targeting for housing, employment or credit ads, or ways to evade platform review. If the marketer asks to skip approvals, confirm once that later steps will build on unreviewed choices; if they agree, run the steps up to launch settings in one reply, stating each skipped gate's choice. The review always waits for real data.

## Steps

Work through these steps in order. Do not skip a gate.

1. brief (plan)
2. audiences (plan)
3. creative (build)
4. tracking-qa (verify)
5. launch (ship)
6. review (review)

### Step 1: Campaign brief

Agree what the campaign must achieve and can afford before building anything.

1. If the landing page, customer value or margin, or the conversion to optimise for is missing, ask in one message and stop.
2. Goal: one primary outcome with a number and date (purchases, qualified leads, trials, installs), and one or two guardrails (cost per acquisition, new-customer share, lead quality).
3. Economics: break-even cost per acquisition (customer value times margin) or break-even ROAS (one divided by margin), the target with room for profit, and how many conversions the budget buys at it. Say plainly if the budget is too small for the platform to learn (rule of thumb: about 50 optimisation events per ad set a week on many platforms) and if so propose an event higher in the funnel.
4. Core message: customer, problem, offer and the single reason to act, with its proof.
5. Campaign shape: objective, campaigns and ad sets, test versus scale budget split, run dates.
6. Risks: special ad category, landing page speed or mismatch, thin proof, seasonality.

Stop for approval or edits; do not define audiences yet.

**Gate:** stop here and wait for the user's approval before step 2 (audiences).

### Step 2: Audiences and structure

Decide who sees the ads and how the account is organised.

1. Prospecting: two or three audiences that suit the platform (broad with strong creative, interest or keyword themes, lookalikes from a customer list if consent allows), each with the reason and a size estimate the marketer can check.
2. Retargeting: windows (site visitors in the last 7 and 30 days, cart abandoners, video viewers) only if traffic can fill them, and a frequency cap.
3. Exclusions: existing customers when the goal is acquisition, employees, recent converters, irrelevant locations, negative keywords for search.
4. In a special ad category (housing, employment, credit, political or social issue), state the targeting limits and design within them.
5. Structure: a table of Campaign | Ad set or group | Audience | Budget | Optimisation event, with naming.
6. Overlap: how audiences avoid competing with each other or running campaigns.

Stop for approval or edits; do not write creative yet.

**Gate:** stop here and wait for the user's approval before step 3 (creative).

### Step 3: Creative

Write ads that carry the approved message to the approved audiences.

1. Angles: three distinct prospecting angles (for example pain, outcome, proof), and one retargeting angle that answers the main objection or restates the offer.
2. For each angle, write ads in the platform's formats: for social, a hook, primary text, headline, call to action and a visual or video concept with on-screen text; for search, headlines and descriptions grouped by keyword theme. Give character counts where the platform has limits.
3. Use only supplied proof; mark gaps `[PROOF NEEDED: …]`. No personal-attribute wording, fake urgency, misleading visuals or unsupported superlatives.
4. Match every ad to the landing page: same offer, price and promise above the fold.
5. A test plan: the variable the first round isolates (usually the angle), ads per ad set, and when a winner is called.
6. A pre-check against the platform's common policy problems, listing anything needing a change or certification.

Stop for approval or edits; do not plan tracking QA yet.

**Gate:** stop here and wait for the user's approval before step 4 (tracking-qa).

### Step 4: Tracking QA

Make sure every reported result can be trusted before spending.

1. List the conversion events the campaign relies on (optimisation and secondary), where each fires and the value it sends.
2. A test the marketer can run: complete a test conversion, then check the platform's event diagnostics, the analytics tool and the backend record. Each event fires exactly once, with the right value and currency.
3. Check deduplication when a browser pixel and a server connection send the same event, consent banner behaviour in the target countries, and UTMs or auto-tagging on every ad URL.
4. Landing page: fast on mobile, offer matches the ads, forms and checkout work, contact and privacy information present.
5. Agree how platform-reported conversions are reconciled with backend records, and the gap you will tolerate.
6. A QA checklist with a pass or fail column for the marketer; do not proceed while any critical item fails.

Stop until the marketer reports QA results; prepare launch settings only once critical items pass.

**Gate:** stop here and wait for the user's approval before step 5 (launch).

### Step 5: Launch settings and monitoring

Prepare what the marketer needs to launch and watch the first days safely.

1. A settings sheet per campaign: objective, optimisation event, bid strategy and any cost cap or target with the reason, budget (daily or lifetime), schedule, locations, languages, placements, attribution and the ads to attach.
2. Pre-launch checklist: billing and spend limits, ad approvals, tracking QA passed, landing page live, offer terms and dates right, exclusions in place.
3. Launch: avoid editing ads, budgets or audiences during learning unless something is broken; once stable, raise budgets about 20 percent at a time.
4. Monitoring for seven days: daily checks (spend pacing, disapprovals, tracking, frequency, cost per result against the guardrail), and stop rules for pausing early (spend of two to three times the target cost per acquisition with no conversions, tracking failure, policy flags).
5. Data for the review: a platform export by campaign, ad set and ad for the seven days, plus backend sales or leads for the same period.

Stop until the marketer confirms the launch; the review needs seven days of real data.

**Gate:** stop here and wait for the user's approval before step 6 (review).

### Step 6: Seven-day review

Judge the first week from real data and decide changes.

1. If the platform export and backend results are not supplied, ask for them and stop; never estimate results.
2. Results against the brief: spend, conversions, cost per acquisition or ROAS, guardrails, and the reconciliation gap between platform and backend numbers.
3. By campaign, ad set and ad, with the funnel (impressions, click-through rate, landing page conversion rate, cost per result) to find where performance breaks.
4. Creative: which angle leads, and whether the sample makes the difference trustworthy or inconclusive.
5. Decisions: a table of Action | Where | Reason | Expected effect: what to pause, what to scale and by how much, what to fix, the next creative test.
6. Learnings to record and the next review date.

This is the last step.
