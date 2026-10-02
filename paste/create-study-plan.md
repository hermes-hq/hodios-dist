<context>
Plans fail for predictable reasons: they assume more hours than exist, treat every topic as equal, leave review and practice tests for the last week, and have no slack, so one missed day collapses the schedule. The evidence-backed shape is: learn each topic with retrieval practice instead of rereading, revisit it at growing intervals, interleave topics once they are learned, and finish with timed practice under exam conditions.
</context>

<task>
Build a study plan for **[EXAM]** on **[EXAM_DATE]**, with 10 hours per week.

Topics:
<topics>
[TOPICS]
</topics>

1. Establish today's date. If you do not reliably know it, ask for it and stop. Count the days and weeks available and the total study hours.
2. Weight each topic: exam weight (from the input, or equal weights if none are given) multiplied by need (low confidence counts about double, high confidence about half). Turn the weights into hours.
3. Divide the time into phases:
   - **Learn** (about the first 55%): new topics in a sensible order, prerequisites first. Every session ends with 5 to 10 minutes of self-testing.
   - **Consolidate** (about 25%): mixed practice across topics, focused on the weakest ones.
   - **Exam practice** (about the last 20%): at least two full timed practice exams, each followed by a review session of its mistakes.
4. Schedule spaced reviews of each topic roughly 1, 3, 7, 14 and 30 days after it is first studied, as short sessions (15 to 25 minutes), dropping the ones that fall after the exam.
5. Add slack: keep about 10% of each week unassigned as buffer, plus one or two buffer days before the final week. The day before the exam is light review and rest, with no new material.
6. Use sessions of 25 to 50 minutes, and say which activity each one is for (self-test, practice problems, flashcards, past paper, error review), not just "study X".
</task>

<constraints>
- If fewer than 7 days remain, switch to a triage plan: rank the topics by marks per hour and say plainly which ones to drop.
- If the exam date is in the past or cannot be parsed, ask for it and stop.
- If the available hours cannot cover the topics at even a basic level, say so in the Budget section and show what fits.
- Do not invent exam weights or the syllabus. Mark every assumption you make.
- Plans longer than 6 weeks: write the first 2 weeks day by day and the rest week by week.
</constraints>

<output_format>
## Assumptions
Bullets: today's date, study days per week, weights you assumed.
## Budget
A table: Topic | Weight | Confidence | Hours | Share of total. Then one line: total hours available vs. allocated.
## Schedule
A table: Date | Minutes | Topic | Activity | Phase. Mark review sessions "Review" and buffer slots "Buffer".
## If you fall behind
Three bullets saying what to cut first, what never to cut (spaced reviews and practice exams), and how to use the buffer.
</output_format>
