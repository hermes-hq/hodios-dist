---
name: write-user-stories
description: Turns a feature description into small, independent user stories for specific users, each with acceptance criteria, and splits stories that are too big. Use when preparing a backlog.
license: CC0-1.0
arguments:
  - feature
  - users
  - story_format
  - with_criteria
argument-hint: <feature> [users] [story_format] [with_criteria]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: product
  source: https://hermes-ide.com/prompts/write-user-stories
  catalog: 2026.1002.1
---

# Write user stories

## Inputs

- `feature` (required): The feature, PRD excerpt or problem to turn into stories.
- `users` (optional): The user types involved (for example shopper, store admin, support agent).
- `story_format` (optional; one of: connextra, job-story; default: connextra): connextra is "As a …, I want …, so that …"; job-story is "When …, I want to …, so I can …".
- `with_criteria` (optional; default: true): Add acceptance criteria to every story.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A user story is a small promise of value to a specific user, sized to finish in a few days and testable on its own. Stories go wrong when they describe technical tasks ("create the table"), when the user is a vague "user", or when one story hides a whole feature.
</context>

<task>
Write user stories for: $feature
Only if users was provided: 
Users involved: $users
Format: $story_format.

1. Identify the user types and the journey they go through for this feature. Group the stories by journey step.
2. Write one story per piece of user-visible value. Each must be independent, negotiable, valuable, estimable, small and testable (INVEST).
3. Split any story that is too big, using the pattern that fits: workflow steps, business rule variations, data variations, happy path before error paths, simple before complex, or one operation at a time. Note which pattern you used.
Only if with_criteria was provided: 
4. Under each story, write 2 to 5 acceptance criteria as Given/When/Then, with concrete example values, covering the main path and the most likely failure.
</task>

<constraints>
- Name a specific user type in every story. Use "user" only if there truly is a single kind of user.
- No technical tasks as stories. If technical work is needed, mention it in the story's notes.
- Do not invent business rules (limits, prices, permissions). Turn each one you need into an open question.
- At most 15 stories. If the feature needs more, cover the first release and list the rest under Out of scope.
</constraints>

<output_format>
## Stories
For each journey step, a `###` heading, then per story:
**[ID] [Short title]**
The story sentence.
Acceptance criteria (when requested), then Notes if any.
## Split notes
Which stories you split and the pattern used.
## Open questions
Numbered.
## Out of scope
Bullets.
</output_format>
