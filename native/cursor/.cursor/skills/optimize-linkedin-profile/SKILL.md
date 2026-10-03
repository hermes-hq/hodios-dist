---
name: optimize-linkedin-profile
description: Rewrites a LinkedIn headline, About section and experience entries for a target role, so recruiters find the profile in search and want to reach out. Use before or during a job search.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: resumes
  source: https://hermes-ide.com/prompts/optimize-linkedin-profile
  catalog: 2026.1003.0
---

# Optimize a LinkedIn profile

## Inputs

- [PROFILE] (required): Your current headline, About section, experience entries and skills, pasted as text. A resume works if you have no profile yet.
- [TARGET_ROLE] (required): The role you want recruiters to find you for (for example "senior product designer, fintech").

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a technical recruiter who sources candidates on LinkedIn every day. Recruiters find people by searching titles, skills and keywords, then decide in seconds from the headline, current title and the first lines of the About section whether to open a profile and send a message. Profiles get missed when the headline is a vague tagline ("Passionate about innovation"), when the target title appears nowhere, or when the About section is a third-person bio with no proof.

Target role: [TARGET_ROLE]

<profile>
[PROFILE]
</profile>
</context>

<task>
1. List the search keywords a recruiter would use for [TARGET_ROLE]: the 2-3 job titles in common use, and 10-15 hard skills, tools and domain terms. Mark which ones the profile already shows with evidence and which are missing.
2. Headline: write three options (within the platform's headline limit, currently about 220 characters; check it), each combining the target title or closest honest title, the core specialism, and a proof point or domain. Avoid emoji walls and slogans.
3. About section: rewrite in the first person, 150-300 words. The first two lines carry the value proposition because they show before "see more": who you help, how, with what result. Then 2-3 short proof points, what you are looking for or interested in, and a plain call to connect. Keep the user's voice and facts.
4. Experience: for each entry in the profile, give a one-line role summary (scope: team, product, users, budget) and 3-5 achievement bullets with action, scope and result. Keep the employer's job title accurate; where it is unusual, suggest adding the common equivalent in parentheses only if it honestly describes the work.
5. Skills: list the skills to add or move up (platforms let you feature a few at the top), drawn only from evidence in the profile.
6. Quick wins: other settings and sections that affect search and response (open-to-work visibility choices and their trade-off when currently employed, location, a custom profile URL, a professional photo, featured work, recommendations to request).
</task>

<constraints>
- Do not add titles, employers, skills, numbers or achievements that the profile does not support. Where a result needs a number you do not have, use [X] and add a question.
- Write for humans first; work keywords in naturally, never as a stuffed list in the About section.
- A profile is public and seen by the current employer too; if the user appears employed, keep the language suitable for that and mention the open-to-work visibility choice.
- Character limits on the platform change; mention the limits you assume.
</constraints>

<output_format>
## Search keywords
Table: Keyword | In profile with evidence (yes, weak, no).
## Headline
Three numbered options, each with its character count.
## About
The full rewrite.
## Experience
For each role: title, company, summary line, bullets.
## Skills
## Other quick wins
## Questions
Facts you need to replace every [X] and fill any gap.
</output_format>
