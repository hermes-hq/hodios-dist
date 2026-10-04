---
name: sop-rollout-track
description: Rolls out a new standard operating procedure in gated steps - draft, review with the staff who do the work, train, audit after two weeks and revise - so the procedure is actually followed.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: operations
  source: https://hermes-ide.com/prompts/sop-rollout-track
  catalog: 2026.1004.1
---

# SOP rollout track

## Inputs

- [PROCESS] (required): The process the SOP covers, how it is done today (or how it should be done if new), why it is changing, and any existing document.
- [TEAM] (required): Who will follow it - roles, number of people, shifts or sites, experience, language needs - and who owns the SOP.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Rolls out a standard operating procedure the way an experienced operations manager would: a draft, a review with the people who do the work, training, an audit after two weeks of real use, and a revision based on what the audit found.

<process>
[PROCESS]
</process>

<team>
[TEAM]
</team>

Each step produces one artifact and stops for the owner's approval or edits; later steps build on the approved versions. Steps 2 and 4 need input from the real world (staff feedback, audit observations): ask for it, and if the owner wants to continue without it, label anything you assume as "(assumed, not observed)". Never invent staff feedback, audit results, safety limits, approval thresholds or legal requirements; mark gaps as `[CONFIRM: …]`. If the owner asks to skip approvals, confirm once, then run the remaining steps in one reply and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. draft (build)
2. staff-review (review)
3. train (operate)
4. audit (review)
5. revise (build)

### Step 1: Draft the SOP

Write a first version that the people doing the work can react to.

1. If the trigger, the end state or the roles involved cannot be worked out from the process description, ask for them in one message and stop. Otherwise write the draft and list your assumptions.
2. Write the SOP: purpose (two sentences at most), scope (in and out), roles, what is needed before starting, then numbered steps with one action each, starting with a verb, in the order the work actually happens. Add a check after any step where a mistake is likely or costly, and put warnings before the step they apply to.
3. Add exceptions (what goes wrong and what to do, with who to escalate to) and records (what is logged, where).
4. Mark every unclear value as `[CONFIRM: …]`.
5. Add a short "What is changing" box comparing the new way with the old, so staff see the difference at a glance. If the process is new, say so.
6. List the three to five questions to put to staff in the review (step 2), aimed at the steps most likely to be wrong or skipped.

Stop and wait for approval or edits. Do not plan training yet.

**Gate:** stop here and wait for the user's approval before step 2 (staff-review).

### Step 2: Review with the staff who do the work

Test the approved draft against reality before anyone is trained on it.

1. Give the owner a 20 to 30 minute review session plan: who attends (at least one experienced person and one newer person per role or shift), how to walk through the draft (ideally at the workstation, doing the task), the questions from step 1, and how to capture feedback (Step | Issue | Suggested change | Who raised it).
2. Ask the owner for the feedback. If they have it, go to 3. If they want to continue without a review, warn once that unreviewed SOPs are the ones staff ignore, then mark the revision "(assumed, not observed)".
3. Turn the feedback into a change table: Step | Feedback | Decision (accept, reject, needs owner) | Reason. Accept changes that make the procedure match how the task can safely be done; reject changes that remove a control the owner needs (safety, money, food handling, personal data) and say why.
4. Produce the revised SOP with the changes applied and the `[CONFIRM]` list updated.

Stop and wait for approval. Do not plan training yet.

**Gate:** stop here and wait for the user's approval before step 3 (train).

### Step 3: Train the team

Plan training on the approved SOP so everyone can do it before the go-live date.

1. Choose the format by team: a short demonstration at the workstation for hands-on tasks, a walkthrough for system tasks, a briefing plus a one-page quick reference for simple changes. Fit it to shifts, sites and language needs from the team description.
2. Write the session plan: show (trainer does it, explaining the why), do (each person does it while observed), check (sign-off when done correctly without help). Name the trainer role and how long it takes per person.
3. Write a one-page quick reference card from the SOP: the steps, the checks and who to call.
4. Write a sign-off record: Name | Role | Trained on | Trainer | Competent (Y/N) | Date.
5. Set the go-live date and what happens to the old way (retired documents removed, systems changed), plus a short announcement message to the team that explains why the procedure is changing.
6. Say what the owner should watch in the first week and the date of the two-week audit.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 4 (audit).

### Step 4: Audit after two weeks

Check whether the SOP is followed and whether it works.

1. Give the owner an audit plan: observe the task done by at least two people on different shifts without warning them in a way that changes behaviour, check the records, and ask each person two questions ("What is the hardest step?" and "When do you do it differently?").
2. Provide an audit checklist built from the SOP: each step and each check, marked Followed | Partly | Not followed, with notes; plus records complete (Y/N) and outcome measures (errors, time taken, complaints) compared with before, if the owner has them.
3. Ask the owner for the results. Do not invent them. If they continue without results, give the checklist and stop there.
4. With results, analyse them: for each step not followed, decide the cause - the step is unclear, the step is impractical, the person was not trained, or the person chose not to - because each cause has a different fix (rewrite, redesign, retrain, manage). Use a quick five-whys on the most important gap.
5. Summarise: compliance by step, the top three gaps with their causes, and the recommended changes.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 5 (revise).

### Step 5: Revise and set the review cycle

Turn the audit into the version the team keeps using.

1. Produce the revised SOP with a change log (version, date, what changed, why) and the remaining `[CONFIRM]` items.
2. List follow-up actions that are not document changes: retraining for named roles, equipment or system fixes, management conversations, with owners and dates.
3. Write a short message to the team saying what changed after their feedback and the audit.
4. Set the ongoing cycle: who owns the SOP, a review date (sooner for safety or money processes), the triggers that force an early review (an incident, new equipment, a legal change, repeated errors) and a light spot-check routine.

This is the last step.
