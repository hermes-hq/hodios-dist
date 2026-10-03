---
name: tailor-resume-to-job
description: Tailors a whole resume to one posting by reordering, selecting and rewording experience honestly, then checks keyword coverage for applicant tracking systems. Use before each important application.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: resumes
  source: https://hermes-ide.com/prompts/tailor-resume-to-job
  catalog: 2026.1003.1
---

# Tailor a resume to a job

## Inputs

- [RESUME] (required): Your full current resume as text.
- [JOB_POSTING] (required): The full job posting text.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a recruiter turned resume strategist. A tailored resume is the same true career, edited for one reader: the most relevant evidence moves to the top third of page one, irrelevant detail shrinks, and the wording uses the employer's terms where they honestly describe the work. Applicant tracking systems and recruiter searches match terms, so a missing keyword can hide a qualified candidate; but a skill added without evidence gets found out in the first interview.

<resume>
[RESUME]
</resume>

<job_posting>
[JOB_POSTING]
</job_posting>
</context>

<task>
1. Strategy: name the 3-5 things this employer most needs (from responsibilities and must-haves) and, for each, the strongest evidence in the resume. State the angle the resume should take in one sentence.
2. Tailor:
   - Summary: 2-3 lines that state the candidate's identity in the posting's terms, years and domain, and the two strongest proofs.
   - Skills: reorder so the posting's must-have skills the candidate has come first; remove clutter that is irrelevant to this role.
   - Experience: within each role, reorder bullets by relevance; rewrite the most relevant ones with action, scope and result; shorten or cut bullets that do not support the angle. Keep titles, employers and dates exactly as given.
   - Optional sections (projects, certifications, volunteering): promote one if it fills a gap in the main experience.
3. Keyword coverage: extract the posting's hard skills, tools, certifications and domain terms. For each, mark covered (with where), added (where you reworded true experience into the posting's term), or missing (no evidence). Use the posting's exact spelling, and include both the acronym and the full term for key ones.
4. Format check for applicant tracking systems: standard headings (Summary, Experience, Skills, Education), reverse-chronological order, consistent plain-text dates, no important text in tables, columns, text boxes, headers, footers or images, and a sensible length (one page for early-career, two for most experienced candidates).
</task>

<constraints>
- Honesty first: never add a skill, tool, title, metric or responsibility the resume does not support. A missing must-have goes into Questions ("Have you used X? Where?") or stays a gap.
- Do not change dates, titles or employers, and do not hide a role in a way that creates an unexplained gap; shorten it instead.
- Keyword use must read naturally; no hidden or white text, no keyword lists pasted at the bottom.
- Preserve the candidate's voice; edit, do not rewrite everything.
</constraints>

<output_format>
## Tailoring strategy
Needs-to-evidence table: Employer need | Best evidence | Where it now appears. Then the one-sentence angle.
## Tailored resume
The full resume in plain Markdown, ready to copy into a document.
## Change log
Bullets: moved, cut, reworded, and why.
## Keyword coverage
Table: Keyword | Status (covered, added, missing) | Where or note.
## Format check
Pass or fix for each item.
## Questions
Facts that would let you cover a missing keyword honestly or replace a placeholder.
</output_format>
