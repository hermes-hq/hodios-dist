---
name: open-source-launch-track
description: Takes an open-source project from readiness fixes to a channel plan, per-channel drafts, a launch-day run sheet and a two-week review, pausing for the maintainer's approval between steps.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: product-launch
  source: https://hermes-ide.com/prompts/open-source-launch-track
  catalog: 2026.1004.1
---

# Open-source launch track

## Inputs

- [PROJECT] (required): What it is, who it is for, license, platforms, install path, the README or repo link, current numbers, the team's hours for launch week and any target dates.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs the launch of this open-source project, one approved step at a time:

<project>
[PROJECT]
</project>

First a readiness check of the pitch, README, install path and repo page, then a channel plan sized to the team's hours, then drafts for each chosen channel, then a go or no-go check and launch-day run sheet, and finally a review two weeks later with real numbers. Each step produces one document and stops for the maintainer's approval or edits; later steps build on the approved versions. The assistant never invents facts, numbers, users or quotes, never proposes vote solicitation, vote rings, alternate accounts, astroturfing or cross-post spam, and calls the project open source only if its license is OSI-approved. The maintainer posts everything personally and makes every go or no-go call.

## Steps

Work through these steps in order. Do not skip a gate.

1. readiness (verify)
2. channels (plan)
3. drafts (build)
4. launch-day (ship)
5. review (review)

### Step 1: Readiness

Make sure a visitor from any launch channel can understand the project and get it running before anyone is sent there.

1. If essentials are missing (who it is for, how to install, the license, the README or its text, the team's hours), ask for them in one message and stop.
2. Check and score each item ready, partly or missing:
   - the one-line pitch: a category noun people search for, the audience, one verifiable difference;
   - the README's first screen: what it is, a GIF or screenshot of the real thing, honest status;
   - time to first success: count the steps from landing to a working result, and flag sign-ups, API keys or source builds that come before any value;
   - repo page: description, topics, website, license detected, a tagged release with notes, social preview image, issue templates, a place for questions;
   - capacity: hours available to answer issues and comments in launch week.
3. Write the fixes for every item that is partly ready or missing, ranked by effect, with rewritten text for the pitch, README opener and quick start where needed. Mark facts you cannot verify as [CHECK].
4. Give a verdict: launch on the planned date, or fix the listed blockers first.

Stop and wait for approval or edits. Do not plan channels yet.

**Gate:** stop here and wait for the user's approval before step 2 (channels).

### Step 2: Channel plan

Choose where to launch, using the approved readiness state.

1. Rank the candidate channels for this audience: Show HN, specific subreddits and forums, Lobsters (only with an invite), X, Bluesky, Mastodon, LinkedIn, dev.to or the project blog, Product Hunt, newsletters with real submission paths, awesome lists the project qualifies for, package registries and directories, and the team's own audience.
2. For each, state fit, the rules or requirements that apply (mark rules you have not seen as UNVERIFIED and tell the maintainer to read them), effort, and now, later or never.
3. Set two or three goals tied to use and say how each will be measured without telemetry (release and registry downloads, GitHub traffic and referrers saved daily because GitHub keeps only 14 days, new issue authors, star history as a lagging signal).
4. Lay out a calendar from two weeks before to two weeks after, one big channel per day, sized to the stated hours. Put directory and awesome-list submissions after launch.

Stop and wait for approval or edits. Do not write the posts yet.

**Gate:** stop here and wait for the user's approval before step 3 (drafts).

### Step 3: Drafts

Write the posts for the approved channels only.

1. For each channel, draft in the maintainer's voice, first person, with "I built this" disclosed:
   - Show HN: an eligibility check (including the posting account's HN history), a plain "Show HN: Name – what it is" title, the link that gets people trying fastest, and maker-comment notes covering why, how it works and honest limits; HN asks makers to write the text by hand, so give notes, not finished prose;
   - each community: a different angle per community, respecting its rules, ending with a real question; where a community bans AI-written text, give an outline for the maker to write;
   - social networks: a standalone first post with media, network-appropriate length and alt text;
   - the blog or dev.to: an outline of a build-story article that teaches one real lesson.
2. Write answers to the eight hardest questions the audience is likely to ask, built only from the facts given; mark gaps as [NEED FACT].
3. Write five saved replies for launch week (install trouble, platform not supported, comparison with a named alternative, feature request, license question).

Stop and wait for approval or edits to each draft.

**Gate:** stop here and wait for the user's approval before step 4 (launch-day).

### Step 4: Go or no-go and launch-day run sheet

Confirm the launch is safe to start and plan the day.

1. Ask the maintainer to confirm each blocker from step 1 is fixed, the try path works from a clean machine and a logged-out browser, the release is tagged, and the people answering are available. Do not mark anything done on your own; if an item is not confirmed, recommend a decision and leave it to the maintainer.
2. Write the run sheet for the first channel's day, hour by hour in the maintainer's time zone: post, first comment, monitoring, reply windows, a break, and when to stop for the day.
3. List what to save during the day and the next 14 days: GitHub traffic views, clones, referrers and popular paths (daily), release downloads, registry stats, new issues and their authors, and questions people asked.
4. Remind the rules for the day: reply to everyone, concede valid criticism, correct facts once without arguing, never ask for votes, never use other accounts.

Stop for the maintainer's go or no-go.

**Gate:** stop here and wait for the user's approval before step 5 (review).

### Step 5: Two-week review

Learn from the launch using the numbers the maintainer saved.

1. Ask for the saved data if it is not provided: daily traffic and referrers, downloads, star history, new issue authors, first-time contributors, and the questions and criticism received.
2. Compare each goal with the result and attribute changes to channels using referrers and timing; label attributions that are guesses.
3. List the top five questions and complaints and the README, docs or product fix each one points to.
4. Say which channels to repeat, which to drop and which to try next, and when the next announcement-worthy release could be.
5. Draft short thank-you notes for people and communities that helped, without asking them for anything.

This step ends the track.
