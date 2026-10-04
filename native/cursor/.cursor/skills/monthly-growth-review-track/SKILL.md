---
name: monthly-growth-review-track
description: Runs a monthly growth review for an open-source project, from collecting public numbers to finding the leakiest funnel stage, judging last month's bets and choosing next month's, with approval gates.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: product-metrics
  source: https://hermes-ide.com/prompts/monthly-growth-review-track
  catalog: 2026.1004.3
---

# Monthly open-source growth review

## Inputs

- [PROJECT] (required): The project, its goal for the year, the month being reviewed, the bets made last month with their predictions, and the archived weekly numbers or where to find them.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs this month's growth review for the following project, one approved step at a time:

<project>
[PROJECT]
</project>

First the numbers are collected and checked, then the funnel is diagnosed to find the stage that leaks most, then last month's bets are judged against their written predictions, then two or three bets are chosen for next month with predictions and owners, and finally a short write-up is produced for the maintainers and, if wanted, a public version for the community. Each step stops for approval. The assistant uses only public or owner-visible data, never proposes telemetry in the software or tracking of individuals, never invents numbers, labels every causal claim as evidence or guess, and treats stars as a lagging, gameable signal. Bets must fit the maintainers' real time.

## Steps

Work through these steps in order. Do not skip a gate.

1. collect (review)
2. diagnose (review)
3. judge-bets (review)
4. next-bets (plan)
5. write-up (review)

### Step 1: Collect and check the numbers

1. Ask for anything missing in one message: the month's weekly archive (views, uniques, clones, referrers, popular paths), downloads per channel (release assets, registries, Homebrew), stars gained, dependents, new issue authors, first-time and returning contributors, median time to first response, and what the team shipped or posted. If no archive exists, say which numbers are already lost (GitHub keeps traffic for 14 days) and list the collection commands to set up now.
2. Put the month in one table next to the previous two months.
3. Flag data problems: missing weeks, changed definitions, likely distortions (CI or mirror download spikes, bot clones, bursts of AI-generated issues, star bursts with no matching traffic).

Stop and wait for approval or corrections to the numbers.

**Gate:** stop here and wait for the user's approval before step 2 (diagnose).

### Step 2: Diagnose the funnel

Using the approved numbers:

1. Lay out the funnel for this project: discover (views, referrers), understand (README and docs paths), try (downloads, installs), succeed and return (returning visitors to docs, repeat downloads of new versions, issues from people who clearly use it), contribute (first and second contributions), fund (sponsors).
2. For each stage, give the conversion where it can be computed and its trend over three months. Say plainly where it cannot be computed.
3. Name the stage that leaks most and the evidence. Give at most three likely causes, each labelled evidence or guess, and what would confirm it.

Stop and wait for approval of the diagnosis.

**Gate:** stop here and wait for the user's approval before step 3 (judge-bets).

### Step 3: Judge last month's bets

1. For each bet from last month, restate the prediction that was written down, then the result, and grade it: worked, did not work, inconclusive. If no prediction was written, grade it inconclusive and say so.
2. Separate effect from noise: compare with the recent range, and note other events in the same weeks that could explain the change.
3. Decide for each bet: keep doing, stop, or rerun with a clearer test.

Stop and wait for approval of the grades.

**Gate:** stop here and wait for the user's approval before step 4 (next-bets).

### Step 4: Choose next month's bets

1. Propose up to five candidate bets aimed at the leakiest stage from step 2, each with the expected effect, the hours it costs, and the evidence behind it.
2. Recommend two or three that fit the maintainers' stated time. Prefer compounding work (README and docs fixes, release announcements, integrations, adopter stories, answering new contributors fast) unless a one-off launch is clearly justified.
3. For each chosen bet, write: the action, the owner, the dates, the prediction ("weekly install-page visits from the README rise from 4% to 8%"), and the number that will judge it.
4. Exclude anything that relies on vote solicitation, astroturfing, spam, fake reviews or tracking people.

Stop and wait for approval of the bets.

**Gate:** stop here and wait for the user's approval before step 5 (write-up).

### Step 5: Write-up

1. Write the maintainers' version in under 300 words: headline, the funnel stage in focus, last month's bets and grades, next month's bets with predictions and owners, data problems to fix.
2. If the maintainers want it, write a public community update in under 200 words: what shipped, thanks to contributors by handle, what the project needs help with, without private numbers they do not want to share.

This step ends the track.
