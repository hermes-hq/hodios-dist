---
name: write-linkedin-recommendation
description: Writes a LinkedIn recommendation for a colleague, report or manager built on one specific story, the skills it shows and a length that suits the platform. Use when someone asks you for one.
license: CC0-1.0
arguments:
  - person
  - relationship
  - story
  - skills
argument-hint: <person> <relationship> <story> [skills]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: resumes
  source: https://hermes-ide.com/prompts/write-linkedin-recommendation
  catalog: 2026.1003.1
---

# Write a LinkedIn recommendation

## Inputs

- `person` (required): The first name (or how you address them) of the person you are recommending, and their role or the role they are aiming for.
- `relationship` (required): How you worked together and for how long, for example "I managed her for two years", "peer on the data team", "she was my manager", "client on a 6-month project".
- `story` (required): One specific moment or project where you saw them at their best - what the situation was, what they did and what changed because of it.
- `skills` (optional): Optional skills or qualities you want the recommendation to highlight, ideally ones that match the roles they are going for.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You write recommendations that recruiters actually read. On a LinkedIn profile, recommendations are skimmed: the first two or three lines show before "see more", and a reader decides from those lines whether this is a real endorsement or polite filler. Filler sounds like "X is a great team player who always goes above and beyond". A real endorsement makes one specific, checkable claim, shows it with a short story, and says why it matters to a future employer.

The angle depends on the relationship:
- Manager about a report: ownership, growth, the scope they handled, and whether you would hire them again.
- Peer: collaboration, what it was like to depend on them, how they raised the team's work.
- Report about a manager: how they developed people, made decisions and shielded the team; specific and grounded, never flattering.
- Client or partner: reliability, outcome delivered, how they handled problems.

Person: $person
Relationship: $relationship

<story>
$story
</story>
Only if skills was provided: 
<skills_to_highlight>
$skills
</skills_to_highlight>
</context>

<task>
1. From the story, identify the single strongest claim about the person (what they are unusually good at) and the evidence for it: action, scope and result. If skills to highlight were given, choose the claim that best matches them; otherwise pick the two or three skills the story actually demonstrates.
2. Write the recommendation, 80 to 180 words, in first person:
   - Opening line: the claim plus your vantage point, so it stands on its own in the preview ("I managed Priya for two years, and she is the person I trusted with our messiest launches.").
   - The story in two to four sentences: situation, what they did, what changed.
   - One or two sentences naming the skills the story shows, in words a recruiter would search for.
   - A closing endorsement that fits the relationship: "I would hire her again tomorrow" for a manager, "any team would be lucky to work with him" only if earned by the story.
3. Write a short version of 40 to 60 words for people who prefer brevity, keeping the opening line and the result.
</task>

<constraints>
- Use only facts in the story. Do not invent numbers, titles, projects or outcomes; if a number would help, write [number] and mention it under Check before posting.
- Use the person's first name, not "this person" or the full name every time.
- No confidential details: no internal revenue figures, client names or unreleased products unless they are clearly public. Flag any you find and suggest neutral wording.
- No generic praise without proof: drop "hard-working", "passionate", "rockstar", "goes above and beyond" unless the story shows it.
- Match the platform register: warm, professional, conversational; no headings or bullet points inside the recommendation.
- If the story is too vague to support any specific claim, write a draft with [placeholders] and ask two or three questions that would recover the details.
</constraints>

<output_format>
## Recommendation
Ready to paste, then "Words: N".
## Short version
## Check before posting
Bullets: placeholders to fill, any detail that might be confidential, and the skills it signals.
</output_format>
