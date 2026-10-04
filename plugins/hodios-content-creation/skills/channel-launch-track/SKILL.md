---
name: channel-launch-track
description: Launches a YouTube channel in gated steps from niche and audience to positioning, content pillars, ten video ideas, first-video packaging and a publishing rhythm. Use before the first upload.
license: CC0-1.0
arguments:
  - creator_background
  - goals
  - time_per_week
argument-hint: <creator_background> [goals] [time_per_week]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: video
  source: https://hermes-ide.com/prompts/channel-launch-track
  catalog: 2026.1004.2
---

# Channel launch track

## Inputs

- `creator_background` (required): What you know, have done or can show on camera; topics you could talk about for years; gear, budget and whether you want to be on camera.
- `goals` (optional): What the channel should achieve and by when, for example a side income, clients for a business, a portfolio, or a community.
- `time_per_week` (optional): Hours per week you can realistically spend on the channel, for example "6 hours, mostly weekends".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Launches a YouTube channel for a creator with this background: "$creator_background". Goals: "$goals". Time available: "$time_per_week". The track moves one approved decision at a time: the viewer, the positioning, the pillars, ten video ideas, the first video's packaging, and a publishing rhythm the creator can keep. Each step produces one artifact and stops for approval; later steps build on approved versions and never re-open settled decisions without asking. The approved viewer and promise are the test for everything after them. The creator owns every decision. Never invent audience data, competitor channels, search volumes or the creator's experience; turn anything uncertain into a quick check the creator can do. If the creator asks to skip the approvals, confirm once that later steps will build on unreviewed choices; if they agree, run the remaining steps in one reply and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. niche-audience (discover)
2. positioning (plan)
3. pillars (plan)
4. video-ideas (design)
5. first-packaging (build)
6. publishing-rhythm (plan)

### Step 1: Niche and audience

Find a niche where the creator's credibility, lasting interest and a real audience overlap.

1. In one message, ask for anything not already given: goals and timeframe, hours per week, what they could make 50 videos about without running dry, what they can show rather than just say (skills, projects, access, results), whether they will be on camera, the language they will publish in, and two or three channels they watch in the space.
2. When you have the answers, propose three niche options. For each:
   - **Viewer:** one sentence naming a specific person and the situation they are in ("renters in their first flat who want it to feel like home without losing the deposit").
   - **What they want:** the outcome, problem or feeling they come to YouTube for.
   - **Why this creator:** the credibility or access that makes them worth watching.
   - **Depth test:** five quick topic examples, to show the niche will not run out in ten videos.
   - **Demand check:** two quick checks the creator can do (search the viewer's questions on YouTube; look for small channels with recent videos far above their usual views). Never state demand as fact.
   - **Path to the goal:** how this niche could reach the stated goal (ads, sponsors, clients, products).
3. Recommend one option and say what would change your mind.

Stop and wait for the creator to choose or adjust the niche and viewer. Do not write positioning yet.

**Gate:** stop here and wait for the user's approval before step 2 (positioning).

### Step 2: Positioning

Position the channel for the approved viewer so a stranger understands in five seconds why to subscribe.

1. Write the channel promise in one sentence: for [viewer] who want [outcome], this channel [does what], unlike [what they find now], because [the creator's credibility].
2. Name the differentiator: the one thing this channel does that comparable channels do not (a method, a format, a point of view, access, a personality). If there is none yet, say so and offer two ways to build one.
3. List what the channel will not cover, so topics stay on promise.
4. Write the channel tagline (under 10 words), the banner line, and a channel description: the first 150 characters say who it is for and what they get; then the upload rhythm and a call to subscribe. Use `[CADENCE]` until step 6 sets it.
5. If the creator has no name yet, give five name options with the trade-off of each and remind them to check handle availability.

Stop and wait for approval or edits. Do not write pillars yet.

**Gate:** stop here and wait for the user's approval before step 3 (pillars).

### Step 3: Content pillars

Turn the approved positioning into three or four content pillars.

1. For each pillar give: its name, the viewer need it serves, how viewers find it (search for a problem, browsing for entertainment, suggested next to similar videos), the typical format (tutorial, test, story, breakdown, challenge, review), and three example topics.
2. Make at least one pillar a repeatable format with a recognisable promise and title pattern, because a series teaches viewers what to expect and turns viewers into subscribers.
3. Give a starting mix (for example 50% search-led help, 30% series, 20% personality) and why it suits the goal.
4. Flag any pillar that needs resources the creator does not have yet.

Stop and wait for approval or edits. Do not generate video ideas yet.

**Gate:** stop here and wait for the user's approval before step 4 (video-ideas).

### Step 4: First ten video ideas

Generate ten video ideas from the approved pillars, ordered as a launch sequence.

1. For each idea give: a working title (under 60 characters), the pillar, the one-sentence promise, the discovery path (search or browse), the format, the effort in hours against the weekly time, and the proof it needs (footage, results, examples), marked as available or still needed.
2. Every idea must serve the approved viewer. Drop any idea that only the creator would click.
3. Order them so the first three show the channel promise most clearly, at least half are findable through search, and the hardest productions come later.
4. Recommend the first video and say why in two sentences.
5. Never assume experiences or footage the creator has not mentioned; mark such ideas "needs: …".

Stop and wait for the creator to approve the list and the first video. Do not package it yet.

**Gate:** stop here and wait for the user's approval before step 5 (first-packaging).

### Step 5: Packaging for the first video

Package the approved first video so the right viewer clicks and is not disappointed.

1. Write six title and thumbnail pairs. The thumbnail shows and the title tells; they do not repeat the same words.
   - Title: under 60 characters, the words a viewer would search or react to first.
   - Thumbnail: one focal subject, at most four words of text, high contrast, readable at phone size. Describe the composition, the expression or key object, and the text.
2. For each pair, name the curiosity mechanism (result, contrast, mystery, stakes, before and after) and the payoff the video must deliver, ideally in the first minute.
3. Write the first 15 seconds for the strongest pair: what is on screen at 0:00 and the spoken lines, with no greeting or channel intro before the hook.
4. Recommend two pairs to test against each other and say what each tests.

Stop and wait for the creator to choose a package. Do not plan the schedule yet.

**Gate:** stop here and wait for the user's approval before step 6 (publishing-rhythm).

### Step 6: Publishing rhythm

Set a publishing rhythm the creator can keep for at least three months with the time they actually have.

1. Estimate hours per video for each phase (idea and research, script, filming, editing, packaging) for the formats chosen, and compare the total with the weekly time. Set the cadence from that maths, not ambition; if even one video every two weeks does not fit, say what to simplify.
2. Propose a batching routine (for example script two videos one week, film both the next weekend) and a buffer: how many finished videos to hold before the first upload.
3. Lay out a 12-week calendar for the ten approved ideas with publish dates, the batch each belongs to, and where optional Shorts cut from the long videos fit.
4. Say what to measure and when: click-through rate and average view percentage per video against the channel's own average, returning viewers, and subscribers per thousand views; judge the direction after ten videos, not after one.
5. Set two review points (after video 5 and video 10) with the questions to ask at each, and the signals that mean change a pillar, the packaging or the cadence.
6. Fill in the `[CADENCE]` placeholder from step 2 and list anything still open.
