---
name: event-visual-identity-track
description: Builds a visual identity for a conference, festival or campaign in gated steps - concept, key visual, templates, signage and wayfinding, social assets and an on-site checklist.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: graphic-design
  source: https://hermes-ide.com/prompts/event-visual-identity-track
  catalog: 2026.1004.0
---

# Build an event visual identity

## Inputs

- [EVENT] (required): The event or campaign - name, purpose, format and size (for example "two-day developer conference, 800 attendees, one venue with three stages"), the host organisation's brand, sponsors, and any fixed elements.
- [AUDIENCE] (required): Who attends or is targeted, for example "backend engineers and engineering managers in Europe".
- [DEADLINE] (required): The event or launch date and the date by which print must go to production, for example "event 12 March; print deadline 20 February".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Builds an event identity that is recognisable from the first announcement to the last slide, flexible enough for dozens of assets made by different people, and practical on site. Event identities fail when the key visual looks good on one poster but breaks on a 1:1 social card, a lanyard and a 3-metre banner; when templates are missing so every speaker and sponsor improvises; and when wayfinding is designed last and printed too late. This track works backwards from the print deadline and pauses for approval after each step.

Event: [EVENT]
Audience: [AUDIENCE]
Deadline: [DEADLINE]

Throughout: work within the host organisation's brand where it exists (the event identity can extend it but must not contradict it), design the key visual as a system that scales, keep accessibility in every asset (contrast, readable sizes at viewing distance, captions and alt text), and show the schedule backwards from the print deadline at every step so it stays realistic. Never use other organisations' logos or artwork without permission, and use placeholders for sponsor logos. If the event description lacks the format, size or venue details a step needs, ask before designing that step. Stop at the end of each step and wait for approval.

## Steps

Work through these steps in order. Do not skip a gate.

1. concept (plan)
2. key-visual (design)
3. templates (design)
4. signage-and-wayfinding (design)
5. social-assets (design)
6. on-site-checklist (ship)

### Step 1: Concept

Find one idea the whole identity grows from.

1. Summarise the brief: purpose, audience, tone, the host brand's fixed elements, sponsor obligations, and every channel (web, email, social, slides, print, venue, stage screens, merchandise, video).
2. Build a timeline backwards from the deadline: print delivery, final artwork, template hand-off, key visual and concept approval. Flag if time is too short and what to cut.
3. Propose three directions, each with a name, the idea and why it fits this audience, the visual language (shape, type, colour mood, imagery), how it scales from a wristband to a stage backdrop, and its risk. Recommend one.

Stop. Ask the user to choose or combine a direction.

Save this step's result to `concept`.

**Gate:** stop here and wait for the user's approval before step 2 (key-visual).

### Step 2: Key visual

Turn the concept into a system, not a single image.

1. The core graphic element (pattern, shape language, typographic device, illustration or photo treatment) and how it varies while staying recognisable.
2. The event lock-up (name, dates, host logo) with clear space, minimum size and a small-use version.
3. Palette with roles and its relation to the host brand, contrast pairs to verify, and display and text faces.
4. Scaling notes for a square social card, a vertical story, a 16:9 stage screen, a badge and a large banner.
5. If imagery is needed, a short brief for a designer or image generator, without naming living artists.

Stop. Ask the user to approve the key visual.

Save this step's result to `key-visual-spec`.

**Gate:** stop here and wait for the user's approval before step 3 (templates).

### Step 3: Templates

Give everyone who makes assets a template, so the identity survives many hands.

1. List templates by when they are needed: announcement, web hero and email header, speaker card, slide deck, sponsor kit, badge, programme, certificates, video title cards and lower thirds.
2. For each: format, fixed and editable areas, text limits, users (staff, speakers, sponsors, volunteers), the tool non-designers will edit it in, and the due date.
3. Sponsor rules (logo size per tier, clear space, neutral panels) and speaker slide guidance (minimum text size for the room, contrast, event title and closing slides).
4. Accessibility: readable sizes, contrast, alt text fields, caption-safe areas.

Stop. Ask the user to approve the template set.

Save this step's result to `template-set`.

**Gate:** stop here and wait for the user's approval before step 4 (signage-and-wayfinding).

### Step 4: Signage and wayfinding

Help people find their way and feel the identity in the venue.

1. Ask for the venue plan if missing: entrances, registration, rooms, catering, toilets, accessible routes and lifts, quiet room, first aid, exits.
2. Map key journeys (arrival to registration, to the main stage, between sessions, to food and toilets) and mark decision points.
3. Define the sign family (welcome banners, directional, room IDs, schedules, information and code of conduct, sponsor, stage backdrops) with sizes and mounting.
4. Legibility: letter heights for viewing distance (state the rule of thumb), high contrast, conventional arrows and pictograms, room names matching the programme, mounting heights that work for wheelchair users.
5. A sign schedule (number, type, location, message, size, quantity, material) plus blank panels for last-minute changes.

Stop. Ask the user to confirm venue details and the schedule.

Save this step's result to `sign-schedule`.

**Gate:** stop here and wait for the user's approval before step 5 (social-assets).

### Step 5: Social assets

Plan the assets that announce the event, build momentum and carry it live.

1. Phases: save the date, tickets or call for speakers, programme reveals, countdown, live, highlights and thanks.
2. Assets per phase in the formats the audience's platforms use, each mapped to a template, with variety rules so the feed is consistent but not repetitive.
3. Accessibility: alt text, captions on all video, no essential text only inside images.
4. A shareable kit for speakers, sponsors and attendees with instructions.

Stop. Ask the user to approve the social plan.

Save this step's result to `social-kit`.

**Gate:** stop here and wait for the user's approval before step 6 (on-site-checklist).

### Step 6: On-site checklist

Make sure what was designed is what appears on the day.

1. Production tracker for every printed item: quantity, supplier, proof date, delivery date, owner; highlight anything past the print deadline.
2. Proof checks: dates, times, room names, sponsor tiers, speaker name spelling, contrast on a printed proof, QR codes tested.
3. Install plan, screen content tested on the real screens, and an on-the-day kit (blank signs, markers, tape, spare schedules, printer and venue contacts).
4. Afterwards: collect photos for highlights and archive files and templates.

Output: tick boxes grouped by day before, morning of and after, ending with the three things most likely to go wrong on site and the backup for each.

Save this step's result to `on-site-checklist`.
