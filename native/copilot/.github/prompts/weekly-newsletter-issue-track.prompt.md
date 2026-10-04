---
description: Produces one newsletter issue in approved steps, from collecting ideas and picking the lead to drafting, editing, subject lines, a test send and a numbers review a week later.
agent: agent
argument-hint: newsletter issue_date inputs
---

# Weekly newsletter issue track

Produces the ${input:issue_date:The date this issue goes out (for example "Thursday 9 October").} issue of this newsletter one approved step at a time:

<newsletter>
${input:newsletter:The newsletter's name, audience, usual format and length, sending day, and one or two past issues for voice.}
</newsletter>

Each step ends with one artifact and waits for the writer's approval or edits. Later steps build on the approved version and do not reopen settled choices without asking. The writer's notes, opinions and voice are the material: the assistant shapes and drafts, and marks every missing fact, link or story with `[ADD: …]` instead of inventing it. If the writer wants to skip the gates, confirm once that later steps will build on unreviewed choices; if they agree, run the remaining production steps in one reply, state the choice made at each skipped gate, and leave the numbers review for after the send.

## Steps

Work through these steps in order. Do not skip a gate.

1. collect (plan)
2. pick-lead (plan)
3. draft (build)
4. edit (review)
5. subject-lines (build)
6. test-send (ship)
7. review-numbers (review)

### Step 1: Collect

Gather everything that could go into the ${input:issue_date:The date this issue goes out (for example "Thursday 9 October").} issue.

<inputs>
${input:inputs:Notes, ideas, links with your comments, announcements and reader replies collected for this issue. Leave empty to gather them in step 1.}
</inputs>

1. If the inputs are empty or thin, ask in one message for: what happened this week that the writer wants to share, links saved with a line on why each matters, announcements or asks, reader replies or questions worth answering, and anything carried over from last issue. Then wait.
2. When there is material, sort it into a candidate list. For each item: a short label, the type (story, idea, link, announcement, reader question), why a reader would care in one line, and what is missing (`[ADD: …]` for an absent link, fact or opinion).
3. Mark items that are time-sensitive for this date and items that could wait for a later issue.
4. Flag anything that needs permission, such as a reader's reply quoted by name.

Stop and wait for the writer to add, cut or approve the list. Do not choose the lead yet.

**Gate:** stop here and wait for the user's approval before step 2 (pick-lead).

### Step 2: Pick the lead

Choose what this issue is about, using the approved candidate list.

1. Propose two lead options. For each: the one-sentence reason to open this issue, the reader it serves, and which other items support it.
2. Recommend one, and say why in a sentence: strongest for the reader, most timely, or most the writer's own view.
3. Propose the running order for the rest: which items become sections, which go in a short links list, and which move to a later issue.
4. Estimate the length against the newsletter's usual length and say if something should be cut.

Stop and wait for the writer to approve the lead and the running order. Do not draft yet.

**Gate:** stop here and wait for the user's approval before step 3 (draft).

### Step 3: Draft

Write the full draft of the ${input:issue_date:The date this issue goes out (for example "Thursday 9 October").} issue from the approved lead and running order.

1. Match the voice of the past issues in the newsletter description: sentence length, formality, humour, how the writer opens and signs off. Do not copy their content.
2. Open with something specific from the lead (a moment, a question, a surprising detail from the notes), and say within the first three sentences what this issue gives the reader.
3. Write one section per approved item with a short heading. Put links inline on the words that describe them, each with a sentence on why it is worth the click, taken from the writer's notes.
4. Close with the writer's usual sign-off and at most one ask (reply, share, an event or product the notes mention).
5. Use only facts, links and opinions from the notes; put `[ADD: …]` wherever something is missing.

Present the draft, then a short list of every `[ADD: …]` item. Stop and wait for the writer's edits or approval.

**Gate:** stop here and wait for the user's approval before step 4 (edit).

### Step 4: Edit

Edit the approved draft as a careful editor would, keeping the writer's voice.

1. Cut: filler openings, repeated points, throat-clearing paragraphs, and any section that does not serve the lead or the reader. Aim for the shortest version that keeps everything worth reading.
2. Tighten: long sentences, vague words ("really", "very", "some"), and headings that do not say what the section gives.
3. Check: every link has an anchor and a reason; every number and name matches the notes; every `[ADD: …]` is either filled by the writer or still flagged.
4. Read it as a skimmer: can someone get the point from the opening, the headings and the bold text alone?
5. Check it suits email: short paragraphs, no tables, alt text for any images.

Return the edited issue, then an edit note: the three most important changes, and anything you cut that the writer may want back. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 5 (subject-lines).

### Step 5: Subject lines and preview text

Write the envelope for the approved issue.

1. Write five subject lines under about 50 characters, each a different approach: the specific lead, a question, a number or detail from the issue, the reader's benefit, and the writer's personal angle. No clickbait, ALL CAPS, false urgency or "Re:" tricks.
2. Write two preview texts under about 90 characters that complement the subject rather than repeat it.
3. Recommend one pairing and say why it fits this list's past style, as described by the writer.
4. If the platform supports a subject line test, suggest which two to test and how the writer will judge them (clicks or replies rather than opens alone, because opens are inflated by mail privacy features).

Stop and wait for the writer to choose.

**Gate:** stop here and wait for the user's approval before step 6 (test-send).

### Step 6: Test send and publish

Prepare the issue to go out on ${input:issue_date:The date this issue goes out (for example "Thursday 9 October").}.

Give the writer a checklist to run in their newsletter platform, tailored to this issue:

1. Send a test to at least two inboxes on different apps, one on a phone. Check images, line breaks, dark mode and that the preview text shows.
2. Click every link in the test email; list the links from the approved issue so the writer can tick them off.
3. Confirm every `[ADD: …]` is gone, names are spelled right, and any quoted reader has agreed.
4. Check the sender name, subject, preview text, segment or audience, and the scheduled time and time zone.
5. Check the footer: unsubscribe link and any address or disclosure the platform or the law where the writer lives requires, and a sponsor label if the issue has a sponsor.
6. After sending: publish the web version if there is an archive, and post a one-line share using the approved subject or lead.

Ask the writer to confirm when it is sent and to note the send date and time. Stop and wait for that confirmation; the next step happens about a week after sending.

**Gate:** stop here and wait for the user's approval before step 7 (review-numbers).

### Step 7: Review the numbers a week later

About a week after the ${input:issue_date:The date this issue goes out (for example "Thursday 9 October").} send, review how the issue did.

1. Ask the writer for the issue's numbers if they have not pasted them: delivered, opens, clicks per link, replies, unsubscribes, spam complaints, new subscribers, and the same figures for the previous three or four issues for comparison.
2. Compare this issue with the recent average, not with outside benchmarks. Treat opens as a rough trend only, because mail privacy features inflate them.
3. Report: which links and sections got clicks (and whether position explains it), replies and what readers said, unsubscribes and complaints against the usual rate, and growth.
4. Name one thing to repeat and one thing to change in the next issue, each tied to a number or a reply.
5. On a small list, say when a difference is too small to mean anything.

End the track with a three-line note the writer can keep in their issue log: what went out, what worked, what to try next.
