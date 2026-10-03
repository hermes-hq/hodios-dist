---
name: prepare-certification-exam
description: Plans preparation for a professional certification from its official domain weights, with a gap check, hands-on labs, practice by domain and a readiness gate. For IT, project and finance exams.
license: CC0-1.0
arguments:
  - certification
  - blueprint
  - experience
  - weeks_available
argument-hint: <certification> [blueprint] [experience] [weeks_available]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: exam-prep
  source: https://hermes-ide.com/prompts/prepare-certification-exam
  catalog: 2026.1003.1
---

# Prepare for a certification exam

## Inputs

- `certification` (required): The exact certification and exam code if there is one, e.g. "AWS Solutions Architect Associate (SAA-C03)", "PMP", "CompTIA Security+", "CFA Level I".
- `blueprint` (optional): Optional official exam guide or outline, pasted, with its domains and weights. Strongly recommended, since outlines are revised.
- `experience` (optional): Optional relevant experience, e.g. "2 years running EC2 and RDS in production, never used networking beyond default VPC".
- `weeks_available` (optional): Optional weeks until the exam and hours per week, e.g. "8 weeks, 6 hours a week".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Certification exams are written to a published blueprint: domains with weights, and task statements describing what a certified person can do. Candidates who fail usually studied what they found interesting rather than what is weighted, relied on reading over doing, or booked the exam before their practice scores were stable. Blueprints are revised every few years, so the plan must follow the current version.
</context>

<task>
Plan preparation for $certification.
Only if blueprint was provided: 
<blueprint>
$blueprint
</blueprint>
Only if experience was provided: 
<experience>
$experience
</experience>
Only if weeks_available was provided: Time available: $weeks_available.

1. **Exam at a glance.** From the blueprint if given; otherwise from what you know, clearly labelled "verify against the current official exam guide". Include the domains and weights, question formats, length, delivery and the passing standard as officially published. If you are unsure which version of the exam is current, say so.
2. **Gap check.** For each domain, write 3 or 4 self-check questions that test the task statements ("Could you design a VPC with public and private subnets across two AZs and explain the route tables?"). Then, using the experience given, give a provisional rating per domain (strong, partial, gap) and say what the learner should confirm by answering the self-checks. Without experience details, leave the ratings for the learner to fill in.
3. **Study plan.** Allocate the time by weight multiplied by gap: heavily weighted gaps first, strong domains get review and practice only. Use the official exam guide and the certifying body's own materials as the backbone. Only if weeks_available was provided: Fit it to $weeks_available. If no time was given, lay the plan out as phases with relative hours and ask for the weeks and weekly hours to schedule it.
4. **Hands-on practice.** For technical certifications, list labs per domain that build the skills the questions test, with the outcome to reach in each. Include safeguards: a dedicated practice account, budget alerts, free-tier or sandbox limits, and tearing down resources after each lab. For non-technical certifications, give the applied equivalent (worked case studies, calculation drills, scenario write-ups).
5. **Practice questions.** How to use practice by domain: untimed and explained first, then mixed timed sets, then full timed exams. Every wrong or guessed answer is reviewed against the official reference before moving on.
6. **Readiness gate.** Define when to book or keep the exam date: for example, at least two full timed practice exams from reputable sources, taken on different days, scored comfortably above the published passing standard, with no domain clearly below it. If the gate is not met a week before the exam, recommend rescheduling, if the provider allows it.
</task>

<constraints>
- Never use or recommend exam dumps or recalled live questions: they breach the candidate agreement, can lead to revoked certification, and are often wrong.
- Do not invent domain weights, passing scores or prerequisites. Unknown means "check the official guide".
- Name third-party resources only as optional examples to evaluate, never as endorsements, and prefer official sources.
- If the certification name is ambiguous or retired, ask which exam the learner means.
</constraints>

<output_format>
Use the section headings from the output contract. Exam at a glance and Gap check as tables (Domain | Weight | Self-check questions | Rating). Study plan as a table: Week | Domains | Activities | Hours. Readiness gate as a checklist.
</output_format>
