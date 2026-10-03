---
name: write-workplace-incident-report
description: Writes a factual, blame-neutral report of a workplace accident, near miss, customer, property or security incident, separating observed facts from statements and listing actions with owners.
license: CC0-1.0
arguments:
  - incident_notes
  - incident_type
  - audience
argument-hint: <incident_notes> [incident_type] [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: business-writing
  source: https://hermes-ide.com/prompts/write-workplace-incident-report
  catalog: 2026.1003.2
---

# Write a workplace incident report

## Inputs

- `incident_notes` (required): Everything you know so far, in any order, such as when and where it happened, who was involved, what people saw or said, injuries or damage, and what was done straight away.
- `incident_type` (optional; one of: injury, near-miss, customer, property, security, other; default: other): The kind of incident. Injury covers any harm to a person; near-miss is an event that could have caused harm but did not.
- `audience` (optional; default: manager and HR): Who reads the report, for example "site manager and HR" or "facilities and the insurer".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A workplace incident report is a record that other people act on: a supervisor fixes the hazard, HR supports the people involved, facilities repairs the damage, an insurer or regulator may read it months later. It is useful only if it is accurate, dated, and written so that a reader who was not there can see what happened without being told whom to blame. The common failures are mixing opinion into facts ("he was being careless"), guessing at causes before anyone has looked, leaving out times and locations, recording more personal or medical detail than the reader needs, and listing actions with no owner.

Write as an experienced health and safety or operations coordinator would: neutral, specific, in the past tense, with every statement either observed, reported by a named role, or marked as unknown.
</context>

<task>
Write a $incident_type incident report for $audience from these notes:

<incident_notes>
$incident_notes
</incident_notes>

1. If the notes do not say what happened, or give no indication of when or where, ask for those details in one short message and stop.
2. Check for urgency first. If the notes suggest someone may still be at risk, a hazard is still in place, a person needs medical attention, or a crime may be in progress, say so at the top under Urgent checks before anything else.
3. Sort every statement in the notes into one of three kinds and keep them apart in the report:
   - **observed:** seen or measured directly by the person reporting;
   - **reported:** told to the reporter by someone else, attributed by role ("the shift lead said…");
   - **inferred:** someone's opinion or guess about cause. Move these to "Possible contributing factors (to be confirmed)" and word them as questions for the investigation, never as findings.
4. Rewrite blaming, emotional or judgemental language into neutral description of actions and conditions ("the floor was wet near bay 4; no sign was in place" instead of "the cleaner left it soaking wet as usual"). Record every change under Language changes.
5. Identify people by role or initials unless the audience needs full names, and record only the injury or health information the reader needs (body part, nature as described, first aid given, whether the person went to hospital). Do not diagnose or speculate about medical outcomes.
6. Propose immediate and follow-up actions that follow from the facts (make the area safe, preserve evidence, check similar equipment, support the person, review the procedure). Give each an owner and date if the notes supply them; otherwise use `[need: owner]` and `[need: date]`.
7. Under Notifications, list who has been told and when, and flag whether this type of incident may have to be reported to an external body (for example a workplace safety regulator, insurer, data protection authority or the police) so the reader can check the rules that apply. Do not state that it is or is not reportable.
</task>

<constraints>
- Use only the facts in the notes. Never invent times, names, witnesses, measurements, injuries or quotes; use `[need: …]`.
- No conclusions about fault, negligence, liability or disciplinary outcomes, even if the notes ask for them. A report that blames is less credible and can harm the people involved.
- Keep exact quotes only when they matter to what happened, attributed by role and in quotation marks.
- Use 24-hour or clearly marked times and a full date if given.
- Keep the report under about 600 words; a reader should grasp what happened from the Summary alone.
</constraints>

<output_format>
## Urgent checks
Anything that needs action before the report is filed, or "None identified".
## Incident report
- **Summary:** two or three sentences: what happened, when, where, outcome.
- **Details:** table with Date and time · Location · Incident type · People involved (role) · Reported by · Report date.
- **What happened:** numbered, chronological, factual steps, each marked (observed) or (reported by …).
- **Injuries, damage or loss:** as described, or "None reported".
- **Immediate actions taken:** what was done, by whom, when.
- **Witnesses:** role and a one-line summary of what each saw.
- **Possible contributing factors (to be confirmed):** conditions and questions for the investigation.
- **Actions:** table with Action · Owner · Due date · Status.
- **Notifications:** who has been told, and external reporting to check.
## Language changes
Bullets: original wording → neutral wording, with the reason. "None" if none.
## Missing information
Bullets: each `[need: …]`, with why it matters. "None" if complete.
</output_format>
