---
name: plan-phd-timeline
description: Builds a PhD or multi-year research project timeline with phases, milestones, a chapter and paper plan, buffers and a monthly check-in routine, working back from the end date. For doctoral students.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: research-methods
  source: https://hermes-ide.com/prompts/plan-phd-timeline
  catalog: 2026.1004.1
---

# Plan a PhD or long research project timeline

## Inputs

- [PROJECT_SUMMARY] (required): Your research question or aims, the studies or work packages you expect, methods, what is already done (data, drafts, papers), and anything that depends on other people or seasons.
- [START_AND_END] (required): Start date and the hard end date, for example "started October 2025, funding ends September 2028, submission by December 2028". Say if you are part-time.
- [REQUIREMENTS] (optional): Programme rules and other load - progression reviews or qualifying exams, required papers, coursework, teaching hours, conferences, leave, a job alongside.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Doctoral projects overrun for predictable reasons: ethics and access approvals take months, data collection slips, analysis reveals problems that send work back, journal review and revision cycles take three to twelve months, and writing up is underestimated. A useful plan works back from the hard end date (usually funding or submission), puts the slow external dependencies early, writes continuously instead of saving writing for the end, turns chapters into papers when the programme allows, and holds an explicit buffer. A milestone only helps if it has a date and a done-criterion someone else could check.
</context>

<task>
Build a timeline for this project.
<project>
[PROJECT_SUMMARY]
</project>
Dates: [START_AND_END]
Only if [REQUIREMENTS] was provided: 
<requirements>
[REQUIREMENTS]
</requirements>

1. Establish where the project stands today: the current month (if it is not in the input, ask for it and plan from the assumption you state) and what is already done. Then compute the months remaining, convert to full-time equivalent if part-time or with teaching or a job, and state your assumptions about anything missing.
2. Work back from the end date: reserve the final submission and examination period, then a dedicated write-up and revision phase (normally at least six months full-time equivalent), then a buffer of roughly 15 to 20 percent of the remaining time, then fit the research phases into what is left.
3. Lay out phases (for example foundations and review, approvals and pilot, study or work package 1, 2, 3, synthesis and write-up), putting slow dependencies such as ethics, data access, fieldwork seasons, equipment or recruitment as early as they can go.
4. Set milestones with a month and a done-criterion: programme reviews, approvals, data collection complete, analysis complete, chapter drafts to supervisor, paper submissions, final draft, submission.
5. Map chapters to papers: for each paper, its source chapter or study, target submission month, and a realistic acceptance horizon. If the programme requires published papers, check whether the review cycles fit and say if they do not.
6. Identify the top risks with an early warning sign and a fallback (a smaller study, secondary data, a dropped chapter).
7. Give a monthly check-in routine: the questions to answer, what to bring to the supervisor, and when to re-plan.
8. List concrete tasks for the next 90 days.
</task>

<constraints>
- Do not invent programme rules, deadlines or required numbers of papers. Use what the user gave, and mark the rest as [CHECK WITH PROGRAMME].
- If the plan does not fit in the time available, say so at the top and give options (descope, extension, thesis format change) rather than compressing everything into an impossible schedule.
- Plan for a sustainable workload: no schedule that assumes evenings and weekends as standard capacity, and include leave.
- Keep the plan supervisor-ready: plain dates (month and year), no motivational filler.
</constraints>

<output_format>
## Assumptions
Bulleted, including the current month used and FTE months remaining.
## Phase plan
A table: phase | months | goals | deliverables. Then a text Gantt with one row per phase and one column per quarter.
## Milestones
A table: month | milestone | done when.
## Chapter and paper plan
A table: chapter | source study | paper? | target journal type | submit by.
## Buffers and risks
A table: risk | early warning | fallback.
## Monthly check-in
The routine and its questions.
## Next 90 days
A checklist.
</output_format>
