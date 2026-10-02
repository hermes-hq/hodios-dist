---
description: Sorts a batch of emails into reply, delegate, schedule and archive by your priorities, flags suspicious messages, and drafts the short replies and delegation notes.
agent: agent
argument-hint: emails priorities
---

# Triage an inbox

<context>
Inbox triage is a sequence of fast decisions, one per message: reply now if it takes a couple of minutes, delegate it if someone else should own it, schedule it if it needs real time or a later date, archive it if no action is needed. The value is in getting each decision right against what matters this week, catching the hidden deadline in a long thread, and not letting a phishing email or a vague "quick question" jump the queue.
</context>

<task>
Triage these emails:
<emails>
${input:emails:The emails to triage, pasted one after another with sender, subject, date and body (or a summary of each).}
</emails>
Only if priorities was provided (leave it empty to skip): 
My priorities and delegates:
<priorities>
${input:priorities:Optional notes on what matters this week, key people, and who you can delegate to, for example "closing the Series A; Ana handles invoices; ignore vendor pitches".}
</priorities>

1. If the input contains no recognisable emails, ask for them and stop.
2. For each email, identify the sender, what is being asked of me, any deadline stated in the email, and how it relates to my priorities.
3. Assign exactly one bucket:
   - **Reply:** needs my response and it can be written in about two minutes.
   - **Delegate:** someone else should own it. Name the delegate only if my priorities say who handles this; otherwise write `[who?]`.
   - **Schedule:** needs me but more than a few minutes of work or thought, or not until a later date. Estimate the time it needs and when to do it, before any deadline.
   - **Archive:** information only, newsletters, notifications, resolved threads or requests I have said to ignore.
4. Check each email for signs of phishing or fraud: urgency plus a link or attachment, requests for credentials, payment or gift cards, changed bank details, a sender name that does not match the address, or an unexpected invoice. Give these the bucket "Suspicious" in the triage table instead of one of the four, explain the signs in the Suspicious section and how to verify through a known channel (a number you already have, not one in the email); never draft a reply that complies. A routine invoice from a supplier I already use is not suspicious by itself; changed payment details or an unknown supplier are.
5. Order the triage table by urgency: hard deadlines first, then items tied to my priorities, then the rest.
6. Draft each Reply in under 80 words, and a one or two line forwarding note for each Delegate.
</task>

<constraints>
- Do not invent deadlines, facts or my decisions. Write deadlines as the email states them ("Friday", "5pm tomorrow"); do not convert them to calendar dates you cannot confirm. When a reply needs a decision I have not given, draft it with a `[decide: …]` placeholder.
- Drafts must not commit me to meetings, money or deliverables unless my priorities say so.
- If there are more than 30 emails, triage the 30 most urgent and list the rest by subject with a suggested bucket only.
</constraints>

<output_format>
## Triage
A table: # | From | Subject | Bucket | Why (one line) | Deadline.
## Draft replies
For each Reply item: "#n to <sender>", then the draft.
## Delegate
For each Delegate item: delegate, then the forwarding note.
## Schedule
For each Schedule item: what it needs, time estimate, suggested slot.
## Suspicious
Each flagged email with the warning signs and how to verify it. "None" if none.
</output_format>
