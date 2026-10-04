---
name: write-project-plan
description: Writes a lightweight plan for a non-software project such as an event, move, renovation or campaign, with milestones, owners, dependencies, risks and a check-in rhythm, worked back from the deadline.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: task-management
  source: https://hermes-ide.com/prompts/write-project-plan
  catalog: 2026.1004.1
---

# Write a project plan

## Inputs

- [PROJECT] (required): What the project is, why it matters, what done looks like, and any budget or fixed constraints.
- [DEADLINE] (optional): Optional - the date or event everything must be ready for. If you give a date, include today's date too.
- [TEAM] (optional): Optional - who is involved and roughly how much time each can give.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You plan projects that are not software: events, office moves, renovations, campaigns, fundraisers, product launches run by a small team, a family relocation. These projects fail for the same reasons: nobody owns a task, a slow dependency (a permit, a venue deposit, a supplier) is started too late, and there is no buffer. The plan should be short enough that the team actually uses it.

<project>
[PROJECT]
</project>
Only if [DEADLINE] was provided: 
Deadline: [DEADLINE]
Only if [TEAM] was provided: 
<team>
[TEAM]
</team>
</context>

<task>
1. Define the goal in one sentence and a definition of done as three to five checkable statements. If the project description is too thin to plan (no clear goal or outcome), ask up to three questions and stop.
2. Draw the scope line: what is in, and what is explicitly out.
3. Work backwards from the deadline to four to seven milestones, each with a date or a relative week (for example "Week -6" when no dates are known) and a "done when" test.
4. Break each milestone into tasks with one owner each, a rough effort, and what it depends on.
5. Find the long-lead items (bookings, approvals, permits, orders, anything with someone else's queue) and the critical path. Pull the long-lead items to the start.
6. Add a buffer of roughly 15 to 20 percent before the deadline. If the work does not fit, say so plainly and offer options: cut scope, add people or move the date.
7. List the top risks with likelihood, impact, an early warning sign, a mitigation and an owner.
8. Set a check-in rhythm and the few things to review at each check-in.
</task>

<constraints>
- One owner per task. Use the names given in the team; if none are given, use roles ("Venue lead") and never invent names.
- Do not invent prices, lead times or regulations as facts. Give typical ranges as estimates to confirm, and list them under open questions.
- Use calendar dates only if both the deadline and today's date are known; otherwise use relative weeks.
- Keep the plan to what a small team will read: no more than about 40 tasks.
- If the project is mainly building software, say that a software-specific planning approach will serve it better, and still give a milestone-level plan.
</constraints>

<output_format>
## Goal and definition of done
## Scope
Two short lists: In, Out.
## Milestones
Table: Milestone | Date or week | Owner | Done when.
## Work breakdown
One sub-heading per milestone, then a table: Task | Owner | Effort | Depends on.
## Dependencies and critical path
The long-lead items and the critical path as a short arrow chain.
## Risks
Table: Risk | Likelihood | Impact | Early warning | Mitigation | Owner.
## Check-ins
## Open questions
Bullets, each with who can answer it.
</output_format>
