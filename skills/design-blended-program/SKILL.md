---
name: design-blended-program
description: Designs a blended programme mixing live sessions, self-paced work and on-the-job practice, with sequencing, weekly time load and support. Use for multi-week training that must change practice at work.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: course-design
  source: https://hermes-ide.com/prompts/design-blended-program
  catalog: 2026.1004.2
---

# Design a blended learning programme

## Inputs

- [OUTCOMES] (required): What participants should be able to do by the end, ideally as observable behaviours at work.
- [AUDIENCE] (required): Who takes part, how many, where they work and how much time they can give, e.g. "30 first-line managers across 3 sites, 3 hours a week".
- [WEEKS] (optional; default: 6): Programme length in weeks.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Blended learning is not "some e-learning plus a workshop". Each modality has a job: self-paced work is best for knowledge people can absorb at their own speed and revisit; live sessions are for practice with feedback, discussion of hard cases and accountability; on-the-job assignments are where transfer happens. A good blend runs a repeating weekly rhythm (prepare, practise together, apply at work, reflect), keeps the weekly time load honest, and involves the participant's manager, because what happens after training predicts whether behaviour changes more than the training itself does.
</context>

<task>
Design a [WEEKS]-week blended programme.

<outcomes>
[OUTCOMES]
</outcomes>

Audience: **[AUDIENCE]**

1. If the outcomes are topics rather than behaviours ("communication", "Excel"), rewrite them as 3 to 6 observable outcomes and mark them "rewritten, please confirm". If the time participants can give is unknown, assume about 3 hours a week and say so.
2. **Modality map:** for each outcome decide what goes self-paced, what goes live and what is practised on the job, with a one-line reason tied to what each modality does best.
3. **Weekly rhythm:** define the repeating cycle (for example: self-paced prep early in the week, a live practice session mid-week, an on-the-job assignment, a short reflection or peer check-in at the end).
4. **Week-by-week plan:** for each week the focus, the self-paced items (with minutes), the live session (length, format, main activity), the on-the-job assignment and the reflection prompt. Sequence from foundations to integrated, realistic application, with the last week focused on a capstone application and a plan for continuing.
5. **On-the-job practice:** for each assignment, what the participant does at work, what they bring back, and what the manager does (brief, observe, give feedback).
6. **Support:** facilitator presence, peer groups or learning pairs, how stragglers are noticed and helped (missed live session plan, nudges), and accessibility for self-paced items (captions, transcripts, mobile-friendly).
7. **Time load:** a table of weekly hours per participant, per manager and per facilitator. Flag any week above the stated budget and adjust.
8. **Evaluation:** how you will know behaviour changed at work (observations, work samples, manager ratings, a business measure), not only completion and satisfaction.
</task>

<constraints>
- Every self-paced item has a purpose and a check (a quick retrieval quiz, a submitted reflection, a question to bring to the live session); no "watch this video" with no follow-up.
- Live sessions spend at least half their time on practice or discussion, not presentation.
- Do not exceed the participants' time budget; if the outcomes cannot fit, say what to cut or how many weeks would be needed.
- Do not name specific vendor platforms unless the user did; describe functions (a discussion forum, a video tool).
</constraints>

<output_format>
## Design summary
3 to 5 sentences: the blend, the rhythm and why.
## Modality map
Table: Outcome | Self-paced | Live | On the job | Reason.
## Week-by-week plan
Table: Week | Focus | Self-paced (min) | Live session | On-the-job assignment | Reflection.
## On-the-job practice
Per assignment: task, bring back, manager role.
## Support
Bullets.
## Time load
Table: Week | Participant hours | Manager hours | Facilitator hours.
## Evaluation
Bullets with measures and timing.
## Assumptions
Bullets.
</output_format>
