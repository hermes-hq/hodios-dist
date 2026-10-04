---
name: parental-leave-return-track
description: Guides an employee back from parental leave in gated steps, from keep-in-touch days and the return conversation to a flexible work request, childcare logistics, the first weeks and rebuilt visibility.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: career-growth
  source: https://hermes-ide.com/prompts/parental-leave-return-track
  catalog: 2026.1004.0
---

# Return from parental leave track

## Inputs

- [LEAVE_END_DATE] (required): The date your leave ends and you are due back, and today's date or how many weeks are left, for example "back on 3 March, about 6 weeks from now".
- [ROLE] (required): Your job, level and team, and anything that changed while you were away (new manager, reorganisation, someone covering your work).
- [DESIRED_SCHEDULE] (optional): The working pattern you want on return, if different - fewer days, compressed hours, set finish times, remote days, a phased return. Leave empty if returning to the same pattern.
- [COUNTRY] (required): Country (and state or region) where you work, because leave, keep-in-touch arrangements, flexible-work rights and breastfeeding provisions differ.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Plans one return from parental leave from the employee's side: reconnect before day one, agree the return with the manager, ask for a sustainable working pattern, make childcare solid with a backup, pace the first four weeks, then rebuild visibility so the leave does not stall the career. Each step produces one artifact and stops for approval. (Managers planning someone's return: use plan-return-from-leave.)

Leave ends: [LEAVE_END_DATE]
Role: [ROLE]
Country: [COUNTRY]
Only if [DESIRED_SCHEDULE] was provided: 
<desired_schedule>
[DESIRED_SCHEDULE]
</desired_schedule>

Rules for every step:
- Work back from the leave end date; if the date has passed or is under two weeks away, compress steps 1 to 4 into what can still be done and say so.
- Use only facts the person gave or confirmed; mark gaps as [X] with a question. Ask before assuming a partner, family help or a particular childcare type.
- Rights to keep-in-touch days, flexible work requests, returning to the same job, and breastfeeding breaks differ by country and employer. Name what to check for [COUNTRY] and where (employer policy, HR, the official labour authority); never state them as settled law.
- If the person describes being sidelined, demoted, pressured to resign or treated worse because of pregnancy, leave or caring, say once that this may be unlawful in many places and suggest HR, a union or an employment advice service.
- If exhaustion, low mood or anxiety sounds like more than adjustment (postnatal depression can affect any parent), acknowledge it and suggest a doctor or health visitor. If anything suggests danger to parent or child, point to emergency services or a crisis line first.
- Keep plans realistic for someone with broken sleep: short scripts, few actions per week, defaults they can accept or change.

## Steps

Work through these steps in order. Do not skip a gate.

1. reconnect (plan)
2. return-conversation (plan)
3. flexible-request (build)
4. childcare (plan)
5. first-weeks (operate)
6. visibility (build)

### Step 1: Reconnect before the return

1. Ask in one message for anything missing: how long the leave has been, contact with work so far, how they feel about returning (keen, mixed, dreading), and whether anything at work changed.
2. Explain the keep-in-touch options to check for the country and employer (paid contact days, informal catch-ups, a team lunch, access to email only if they want it), and how to agree them without being pulled into work early.
3. Draft a short message to the manager proposing a catch-up two to four weeks before the return date, with three things to cover.
4. A light reconnect plan for the final weeks of leave: one or two contact points, what to read or skim (team updates, org changes), and what to deliberately not do.
5. A list of open questions to take into step 2.

Output: options to check, the message, a dated reconnect plan, open questions.

Stop for approval.

Save this step's result to `parental-return/01-reconnect-plan.md`.

**Gate:** stop here and wait for the user's approval before step 2 (return-conversation).

### Step 2: The return conversation

1. An agenda for the meeting with the manager: what changed, responsibilities and handback from cover, first-quarter priorities, working pattern, development, and any pay or review cycle missed during leave.
2. Write how the person opens: their intentions in two sentences (committed to the role, what they want the return to look like), in their own words where possible.
3. Questions to ask, including how performance will be judged during the return period.
4. Responses for likely difficult moments: "your role has changed", "we'd like you to take a smaller project for now", "can you be full-time from day one", or silence on the working pattern.
5. A follow-up email confirming what was agreed.

Output: agenda, opening, questions, response table (They say | You say), follow-up email.

Stop for approval.

Save this step's result to `parental-return/02-return-conversation.md`.

**Gate:** stop here and wait for the user's approval before step 3 (flexible-request).

### Step 3: Flexible work request

1. If no change in schedule is wanted, say so in one line, confirm the return pattern, and skip to the gate.
2. Otherwise, check the desired schedule against the role: which tasks need fixed times or presence, which do not, and what coverage would be needed.
3. Name the formal route to check for the country and employer (whether there is a statutory right to request, eligibility, the form or written format, response time and grounds for refusal, how many requests are allowed per year) and whether an informal agreement might be enough.
4. Draft the request: the pattern wanted and start date, how the work and communication will be covered, how success will be measured, an offer of a trial period, and openness to alternatives.
5. Fallback options if the first ask is refused, ranked from closest to the request.

Output: role check, route to verify, the request, fallbacks.

Stop for approval.

Save this step's result to `parental-return/03-flexible-request.md`.

**Gate:** stop here and wait for the user's approval before step 4 (childcare).

### Step 4: Childcare logistics

1. Ask what is arranged (nursery, childminder, nanny, family, a partner's leave) and what is not.
2. A settling-in plan that overlaps the return, ideally starting care one to two weeks before the first workday, with shorter days first.
3. A workday timetable (drop-off, commute, hours, pick-up, buffer), flagging anything that clashes with the step 3 pattern.
4. A sick-day and closure plan: who covers first, second and third, which days each adult can flex, and what to say to work.
5. Breastfeeding or expressing at work, if relevant: what to ask for (time, a private non-bathroom space, storage) and to check what the employer and the law provide.
6. A split of home tasks between the adults involved, if there is more than one.

Output: settling-in plan, workday timetable, backup ladder, requests to make, task split.

Stop for approval.

Save this step's result to `parental-return/04-childcare-plan.md`.

**Gate:** stop here and wait for the user's approval before step 5 (first-weeks).

### Step 5: The first four weeks

1. A week-by-week plan: week 1 relationships and catching up (one-to-ones with the manager and key colleagues, reading, no big commitments); week 2 taking back named responsibilities; week 3 first visible piece of work; week 4 a check-in with the manager on how the pattern and workload are working.
2. Boundaries for the period: finish times, how to say no to late meetings, what to do when childcare calls.
3. Scripts for common moments: "Welcome back, how's the baby, are you getting any sleep?", being asked to stay late on day three, colleagues who assume less ambition now.
4. A small energy plan: the two or three things that make the week workable (meal plan, evening routine, one rest block).
5. Warning signs that the arrangement is not working and what to do about each.

Output: four-week plan, boundaries, scripts, energy plan, warning signs.

Stop for approval.

Save this step's result to `parental-return/05-first-four-weeks.md`.

**Gate:** stop here and wait for the user's approval before step 6 (visibility).

### Step 6: Rebuild visibility

1. Pick two or three pieces of work over the next quarter that matter to the manager and the wider team, and how each can be seen (a demo, a short written update, presenting at a meeting).
2. A stakeholder list: who to reconnect with in the next six weeks, why, and a one-line message to each.
3. A simple weekly wins log to feed the next review.
4. A career conversation for around week 8: what the person wants in the next 12 months and how the working pattern fits with it, with an opening line.
5. A review date to revisit the whole return plan.

Output: visibility plan, stakeholder table (Who | Why | Message), wins log template, career conversation opener, review date.

Save this step's result to `parental-return/06-visibility-plan.md`.
