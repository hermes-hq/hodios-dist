---
name: newsletter-launch-track
description: Launches a newsletter in approved steps, from positioning and format to the welcome email, the first three issues and a 90-day growth plan. Use when starting a newsletter from zero.
license: CC0-1.0
arguments:
  - topic
  - audience
  - platform
argument-hint: <topic> <audience> [platform]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: newsletters
  source: https://hermes-ide.com/prompts/newsletter-launch-track
  catalog: 2026.1004.0
---

# Newsletter launch track

## Inputs

- `topic` (required): What the newsletter is about, what you know or do that gives you something to say, and any notes or past writing you already have.
- `audience` (required): Who it is for, as specifically as you can (for example "new managers in tech", "parents of kids with food allergies").
- `platform` (optional): The newsletter platform if you have chosen one. Leave empty to get a recommendation in step 2.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Launches a newsletter about "$topic" for $audience one approved step at a time: the positioning and promise, then the format, cadence and platform, then the welcome email, then the first three issues, then a 90-day growth plan. Each step produces one artifact and stops for the writer's approval or edits; later steps build on the approved versions and do not reopen settled decisions without asking. The writer's knowledge and voice are the raw material: the assistant shapes, drafts and plans, and marks every place where a story, fact, link or number is needed instead of inventing one. It does not promise subscriber or revenue figures. If the writer asks to skip the approvals, confirm once that later steps will then build on unreviewed choices; if they agree, run the remaining steps in one reply, state the choice made at each skipped gate, and keep every placeholder visible.

## Steps

Work through these steps in order. Do not skip a gate.

1. positioning (plan)
2. format (design)
3. welcome-email (build)
4. first-issues (build)
5. growth-plan (ship)

### Step 1: Positioning

Decide what the newsletter about "$topic" promises, and to whom.

1. Ask the writer, in one message, for anything not already given: their experience or vantage point on the topic, why they want to start it (audience for a business, a career, income, a creative outlet), the hours a week they can give it, two or three newsletters they read and admire in or near the space, and a writing sample for voice.
2. When you have the answers, write:
   - **Reader:** one or two sentences on who the reader is and the job the newsletter does for them (what they get, learn, feel or decide).
   - **Promise:** one sentence in the form "Every [cadence], [what] for [who] so they can [outcome]." Offer three versions and recommend one.
   - **Point of view:** what this writer sees or believes that others in the space do not, drawn from their experience. If it is not yet clear, say so and ask one sharp question.
   - **Neighbours:** how it differs from the newsletters the writer named (from what the writer says about them; do not invent their content).
   - **Name ideas:** five, each with the reasoning; the writer must check availability.
   - **Success at 90 days:** two or three signals tied to the writer's goal (for example reply rate, first paid subscribers, a client enquiry), not vanity counts.

Stop and wait for the writer to approve or edit the positioning. Do not design the format yet.

**Gate:** stop here and wait for the user's approval before step 2 (format).

### Step 2: Format

Design a format for the newsletter about "$topic" that the writer can sustain.

1. Propose a cadence that fits the stated hours with room for a bad week, and say what happens when a week goes wrong (a shorter issue, a planned skip, a reader-question issue).
2. Design the issue template: length range, recurring sections (two to four, each with a name, purpose and rough word count), a standard opening and sign-off pattern, and where links or recommendations go. Include one recurring element that invites replies.
3. Choose the free and paid split only if the writer's goal involves income; otherwise say "free for now" and when to revisit.
4. Platform (the writer's choice, if any: "$platform"): if one is given, note any constraints it imposes on the format. If it is empty, recommend a platform type for the writer's goal (built-in discovery and payments, ownership and custom design, or integration with an existing website), with one trade-off each, and tell the writer to check current pricing and features. Do not quote prices.
5. Set-up checklist: sender name and address, landing page headline and three-bullet description from the approved promise, a simple logo or header, an about page, and the double opt-in setting.

Stop and wait for approval or edits. Do not write the welcome email yet.

**Gate:** stop here and wait for the user's approval before step 3 (welcome-email).

### Step 3: Welcome email

Write the welcome email new subscribers to the newsletter about "$topic" receive right after signing up.

1. Subject line and preview text: under 50 and 90 characters, warm and specific.
2. Body, 150 to 250 words, in the writer's voice from the sample:
   - Thank them and restate the approved promise in one sentence.
   - What to expect: cadence, day, and what an issue contains.
   - Who the writer is in two or three sentences, from their experience.
   - A reply prompt: one easy question about the reader's situation that will also teach the writer about their audience.
   - A deliverability nudge: ask them to move the email to their main inbox or add the address to contacts.
3. Since there are no back issues yet, offer one useful thing now if the writer has it (a resource, a short guide, a favourite piece of their writing) as `[LINK: …]`; otherwise skip it.
4. List placeholders to fill.

Stop and wait for approval or edits. Do not write the first issues yet.

**Gate:** stop here and wait for the user's approval before step 4 (first-issues).

### Step 4: First three issues

Plan and draft the first three issues of the newsletter about "$topic".

1. Plan three issues that together show the range of the approved promise: one that delivers the core value most directly, one that shows the writer's point of view or story, and one that invites participation (a question, a reader poll, a request for stories). Give each a working title and a one-line description, and say why this order.
2. Draft issue one in full, following the approved template and voice: subject line options, preview text, opening, sections, reply prompt and sign-off. A first issue may briefly say why the newsletter exists, but it must still deliver value on its own.
3. Write detailed outlines for issues two and three: section by section, with the specific material from the writer's notes each uses and `[NEEDED: …]` where a story, example, link or fact is missing.
4. Use only the writer's material. Do not invent anecdotes, data, quotes or links; keep every gap as a visible placeholder and list them at the end.

Stop and wait for approval or edits. Do not write the growth plan yet.

**Gate:** stop here and wait for the user's approval before step 5 (growth-plan).

### Step 5: 90-day growth plan

Plan the launch and first 90 days of growth for the newsletter about "$topic" for $audience.

1. **Launch week:** a day-by-day checklist, including a personal note to people who would genuinely want it (written as a short template, with no buying or importing of contact lists and no adding people without consent), posts on the channels where the writer already has presence, and issue one going out.
2. **Signup surfaces:** where the signup link and a one-line pitch go (email signature, social profiles, website, the end of every piece the writer publishes elsewhere), using the approved promise.
3. **Growth tactics** matched to the audience and the writer's hours: pick three from cross-recommendations with similar-sized newsletters, guest posts or podcast appearances, communities where the audience gathers (contributing value first, following each community's rules), a useful lead magnet built from existing material, and a referral ask in each issue. For each: the first concrete action and the weekly time it needs.
4. **Weekly rhythm:** a routine that fits the hours: write, send, one growth action, read and answer replies.
5. **What to measure:** the 90-day signals approved in step 1, plus open and click rates as rough guides only, with when to review (weeks 4, 8 and 12) and what change each signal would prompt.
6. **Before you send issue one:** a final checklist covering test sends to several inboxes and devices, links, the welcome email automation, the unsubscribe link and a physical or business address if the platform or local law requires it.

Do not promise subscriber, open-rate or income numbers.
