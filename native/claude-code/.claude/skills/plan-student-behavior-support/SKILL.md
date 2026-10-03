---
name: plan-student-behavior-support
description: Drafts an individual behaviour support plan from ABC observations, with a hypothesised function, prevention, a replacement skill, responses and data to collect, for review with specialists.
license: CC0-1.0
arguments:
  - observations
  - student_age
  - supports_in_place
argument-hint: <observations> <student_age> [supports_in_place]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/plan-student-behavior-support
  catalog: 2026.1003.0
---

# Plan individual behaviour support for a student

## Inputs

- `observations` (required): ABC notes (antecedent, behaviour, consequence) from several incidents, with times, settings and what adults did. Use initials only.
- `student_age` (required): Age or grade, and setting, e.g. "7, Grade 2 mainstream class" or "14, Year 9, rotates between six teachers".
- `supports_in_place` (optional): Optional supports already tried or in place (seating, visual schedule, check-ins, an existing plan) and how they went.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Behaviour serves a purpose for the student. Most persistent classroom behaviour gets something (attention from adults or peers, an object or activity, sensory input) or avoids something (a task, a demand, a social situation, discomfort). Plans that only add consequences often strengthen the behaviour, for example sending a student out of a task they want to avoid. Effective individual plans are built on a hypothesis about the function drawn from patterns in observations, then change the triggers (prevention), teach a replacement behaviour that gets the student the same thing in an acceptable way, respond so the problem behaviour stops paying off, and collect data to check the hypothesis. A teacher's draft is a starting point for the school's behaviour specialists, special educators or psychologist and the family, not a substitute for a formal functional behaviour assessment where one is needed.
</context>

<task>
Draft a behaviour support plan for a student aged $student_age.

<observations>
$observations
</observations>
Only if supports_in_place was provided: 
<supports_in_place>
$supports_in_place
</supports_in_place>

1. **Important first:** before planning, check the observations for anything that needs immediate action rather than a plan: self-harm or talk of it, harm to others that puts anyone at risk, signs of abuse or neglect, or a disclosure. If any is present, write the safety steps here (who to tell today, what to record, what to do if anyone is in immediate danger), then write only the "Review with the team" section and stop: say the behaviour plan waits until the safeguarding lead has acted, and do not treat the concern as a behaviour to manage.
2. **Behaviour defined:** describe each target behaviour so two observers would agree when it happens (what it looks and sounds like), and its estimated frequency or duration from the notes.
3. **Patterns in the data:** when, where, during what, with whom, and what usually happens straight after. Note the times and settings where the behaviour does not happen; they are clues.
4. **Hypothesis:** a summary statement, "When [antecedent], [student] does [behaviour] in order to [get or avoid what], and this is maintained because [consequence]." Give a confidence level and the evidence for and against, plus one alternative function to rule out.
5. **Prevention:** 3 to 5 changes to antecedents (task design, choice, pre-teaching, visual supports, seating, transitions, relationship-building check-ins) matched to the hypothesis.
6. **Replacement skill:** one acceptable behaviour that serves the same function and is easier than the problem behaviour (for example asking for a break with a card), how it will be taught and practised, and how it will be reinforced every time at first.
7. **Responses:** what adults do when the replacement skill is used, at early warning signs, and when the behaviour happens, so the behaviour no longer gets the student what it used to, with calm, consistent scripts. Include how to help the student calm and how to repair afterwards.
8. **Data to collect:** a simple tally, interval or ABC form, who records it, for how long, and what change in the data would confirm or reject the hypothesis.
9. **Review with the team:** questions for the family, specialists to involve (for example a special educator, behaviour specialist, school psychologist or counsellor) and a review date.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- If the person mentions thoughts of suicide or self-harm, harming someone else, abuse, or being in danger, stop the exercise. Respond with care, tell them they deserve support now, and point them to local emergency services or a crisis line in their country. If you do not know their country, ask, and mention that local emergency numbers work everywhere.
- You are a supportive tool, not therapy. For ongoing distress, low mood that lasts, or anything that disrupts daily life, encourage them to talk to a doctor or a licensed mental-health professional.
- Never shame, diagnose, or tell someone what they "really" feel. Reflect back what they said and offer, rather than impose, next steps.
- The user is a teacher; the safety steps above apply to the student. A student's talk of suicide or self-harm, harming someone, or being harmed goes to the school's designated safeguarding or child-protection lead the same day, and to emergency services if anyone is in immediate danger.
- Never diagnose or suggest a diagnosis (ADHD, autism, trauma, anxiety). Describe what was observed; the team decides whether an assessment is needed.
- Never recommend restraint, seclusion, physical punishment, shaming, public behaviour charts that single the student out, or withholding food, water, toilet access or play as consequences. Physical intervention is only ever under school policy by trained staff to prevent immediate harm.
- Base every claim on the observations. With fewer than about five incidents, say the hypothesis is tentative and lead with data collection.
- Use respectful, person-first language and the student's initials only.
- Fit the plan to the setting: a secondary student with several teachers needs a plan every teacher can follow in under a minute.
</constraints>

<output_format>
## Important first
Safety items and actions, or "No immediate safety concerns found in the notes." If there are safety items, this section and "Review with the team" are the whole response.
## Behaviour defined
Bullets per behaviour.
## Patterns in the data
Table: Antecedent / setting | Behaviour | What happened next | Count.
## Hypothesis
The summary statement, confidence, evidence for and against, alternative to rule out.
## Prevention
Bullets.
## Replacement skill
Skill, how it is taught, how it is reinforced.
## Responses
Table: Situation | What adults do | What adults say.
## Data to collect
Method, who, how long, decision rule.
## Review with the team
Questions, people to involve, review date.
</output_format>
