---
name: build-symptom-log
description: Creates a symptom diary template tailored to a condition, or turns logged entries into a clear, counted one-page summary for a clinician without diagnosing. Use before and after tracking symptoms.
license: CC0-1.0
arguments:
  - condition_or_symptoms
  - entries
argument-hint: <condition_or_symptoms> [entries]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: medical-prep
  source: https://hermes-ide.com/prompts/build-symptom-log
  catalog: 2026.1004.2
---

# Build a symptom log

## Inputs

- `condition_or_symptoms` (required): The condition or symptoms you are tracking, for example "migraines", "IBS flare-ups", "my son's eczema", "dizzy spells".
- `entries` (optional): Your logged entries, in any format. Optional; leave empty to get a template to start logging.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Clinicians make better decisions with a few weeks of consistent records than with a memory of "it's been bad lately". A good diary is quick enough to fill in every day, records good days as well as bad ones, captures what the clinician will ask about, and is summarised honestly: counts and co-occurrences, not conclusions.

Tracking: $condition_or_symptoms
Only if entries was provided: 
Logged entries:
<entries>
$entries
</entries>
</context>

<task>
If no entries were provided, build a template:
1. Choose fields: date and time, symptom, severity 0–10, duration, possible triggers or context (sleep, food, activity, stress, menstrual cycle, weather, as relevant), medicines taken with dose and effect, impact on daily life, and notes. Add fields specific to $condition_or_symptoms (for example aura and nausea for migraine; stool type on the Bristol Stool Scale for bowel symptoms; position and arm for blood pressure readings; peak flow for asthma).
2. Give severity anchors so ratings stay consistent (0 none, 3 noticeable but can carry on, 5 hard to ignore and limits some activities, 7 stops most activities, 10 worst imaginable).
3. Add logging tips: log at the same time each day, record symptom-free days too, log for at least 2–4 weeks, keep it short.

If entries were provided, summarise them for a clinician:
1. Period covered, number of days with entries, and days with no entry.
2. Count accurately: number of episodes, how often per week, severity (range and typical), duration, time of day.
3. Patterns as co-occurrence only: "poor sleep noted the night before on 3 of 5 headache days". List which entries support each pattern.
4. Medicines used: how many days, and the effect the person recorded.
5. Impact on work, school, sleep or activities.
6. Gaps and inconsistencies in the data.
7. Questions for the clinician based on the summary.
Then suggest any fields to add to the template going forward.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- No diagnoses and no causal claims. Triggers are "noted together", never "caused by".
- Never fill in missing data or round counts to make a pattern look stronger. Recount before you write the summary.
- Keep the person's own words for symptom descriptions.
- If any entry describes something that needs prompt attention (rapidly worsening symptoms, a sudden severe headache, chest pain, fainting, blood in vomit or stool, new weakness or numbness, or a very unwell child), say so at the top: contact a doctor promptly or emergency services if it is happening now.
- The clinician summary must fit on one printed page.
</constraints>

<output_format>
Without entries:
## Your log template
A table with the column headings and one example row.
## How to rate severity
## Logging tips
## Get checked sooner if
Short list tied to the symptoms tracked, so the person knows what not to just log.

With entries:
## Summary for your clinician
Period and overview (two lines); table: Measure | Value; patterns noticed, each with its supporting entries; medicines and effect; impact on daily life; gaps.
## Questions to ask
## Get checked sooner if
Short list tied to the symptoms tracked.
</output_format>
