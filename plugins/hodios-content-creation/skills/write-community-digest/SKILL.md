---
name: write-community-digest
description: Writes a digest for a club, school, neighbourhood or association from scattered updates, with events, decisions, volunteer asks and contact points. Use for a weekly or monthly community update.
license: CC0-1.0
arguments:
  - updates
  - community
  - frequency
argument-hint: <updates> <community> [frequency]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: newsletters
  source: https://hermes-ide.com/prompts/write-community-digest
  catalog: 2026.1003.2
---

# Write a community digest

## Inputs

- `updates` (required): Everything to include, pasted as it comes - messages, meeting notes, event details, requests for help, reminders - with dates and names of who to contact.
- `community` (required): Who it is for and how it is sent, for example "parents of Year 3, by email and the class WhatsApp" or "Elm Street residents association".
- `frequency` (optional; one of: weekly, monthly; default: monthly): How often the digest goes out; this sets the date window it covers.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You turn the messy pile of updates that volunteer-run groups produce (committee notes, forwarded messages, half-finished event details, pleas for help) into a digest people actually read. Readers of a club, school or neighbourhood digest skim on a phone for three things: what is happening and when, what was decided that affects them, and what they are being asked to do. They miss anything buried in paragraphs. A good digest leads with what needs action, lists dates in one place with weekdays, makes every volunteer ask specific (the task, the time it takes, the date, who to tell), and is warm without being long. It also protects people: it does not publish private phone numbers, children's full names or photos without consent.
</context>

<task>
Write the $frequency digest for: $community.

<updates>
$updates
</updates>

1. Sort the updates into: action needed (deadlines, sign-ups, payments, forms), dates and events, decisions made, volunteer asks, reminders, thank-yous and good news, contacts. Merge duplicates and drop anything outside the $frequency window unless it is a key upcoming date; list what you dropped.
2. Write three subject line options that name the most important action or event.
3. Write the digest:
   - an opening of one or two sentences with the single most important thing,
   - "Action needed" with deadlines in bold,
   - "Dates" as a list with weekday, date, time, place and who it is for,
   - "Decisions" in plain words, each with what it means for readers,
   - "Help wanted" with each ask as task, time needed, date and how to say yes,
   - "Reminders", "Thank you" and "Contacts" (roles and the contact method given).
4. Write a short version (under 120 words) for a chat group or noticeboard that points to the full digest.
5. List what to check before sending.
</task>

<constraints>
- Use only the information given. Never invent dates, times, places, prices, decisions or names. Where a detail is missing, write `[CONFIRM: …]` and list it at the end.
- Write weekdays with dates and spell out ambiguous dates.
- Do not include private phone numbers, home addresses, children's full names or health details unless the updates clearly say they are for publishing; flag them under Check before sending.
- Keep the tone warm, inclusive and plain; avoid in-jokes and committee jargon newcomers would not understand.
- Skip any empty section rather than filling it.
</constraints>

<output_format>
## Subject lines
Three options.

## Digest
The digest with the headings above.

## Short version
Under 120 words.

## Check before sending
Every `[CONFIRM]` item, anything dropped, and any privacy flags.
</output_format>
