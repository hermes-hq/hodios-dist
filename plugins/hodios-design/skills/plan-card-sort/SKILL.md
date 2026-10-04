---
name: plan-card-sort
description: Plans an open, closed or hybrid card sort with the card set, participants, tool setup, analysis method and how the results feed navigation. Use when restructuring a site or app's information.
license: CC0-1.0
arguments:
  - content_inventory
  - goal
argument-hint: <content_inventory> [goal]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: ux-research
  source: https://hermes-ide.com/prompts/plan-card-sort
  catalog: 2026.1004.2
---

# Plan a card sort

## Inputs

- `content_inventory` (required): The content or features to organise - a list, a sitemap export or a description - plus the product, its users and what is wrong with the current structure.
- `goal` (optional): What the team needs to decide (for example "new top-level navigation" or "do our five existing categories make sense to users"). Optional; it decides open versus closed.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Card sorts go wrong in predictable ways: cards copy the current navigation labels, so participants group by matching words instead of meaning; there are 120 cards and people quit halfway; the sample is colleagues; and nobody planned how a similarity matrix becomes a menu, so the results end up as a pretty dendrogram nobody uses. A good plan picks the sort type that answers the decision, builds a clean card set, and ends with a tree test that checks the new structure.
</context>

<task>
Plan a card sort for this content.

<content_inventory>
$content_inventory
</content_inventory>
Only if goal was provided: 
<goal>
$goal
</goal>

If the inventory is too thin to build a card set (a product name only, no content items), ask up to three questions about the content, the users and the decision, and stop.

1. **Study type.** Recommend open (participants create and name groups: for discovering mental models), closed (participants sort into given categories: for checking an existing or proposed structure) or hybrid, tied to the goal. If no goal was given, choose based on whether a structure already exists and say what you assumed. Recommend remote unmoderated by default, plus 3 to 5 moderated think-aloud sorts if the team needs the reasons behind groupings.
2. **Cards.** Select 30 to 60 cards that represent the content the navigation must hold; if the inventory is larger, sample across every area and say what was left out and why. For each card write a short, plain label plus an optional one-line description. Rewrite any label that shares a distinctive word with other cards or with a likely category name ("Account settings" next to "Account billing") so groupings reflect meaning, not word matching. Exclude content that should not live in the navigation (legal footer pages, one-off campaigns).
3. **Participants.** Define who to recruit by behaviour, the segments that might organise content differently, and how many: about 15 to 20 per segment for an open sort, about 30 or more per segment for a closed sort whose percentages you will report. Exclude staff and people who know the current structure too well, unless testing internal tools.
4. **Setup.** Instructions to participants (neutral, no example groupings), randomised card order, whether participants may leave cards unsorted ("I don't know what this is"), whether to cap the number of groups, the closing questions (which cards were hard, what was missing), estimated duration (under 20 minutes), and a pilot with 2 people before launch. Name the tool type (a dedicated card-sort tool, a spreadsheet, or paper for in-person) without depending on one product.
5. **Analysis plan.** For open sorts: clean and standardise participant group names, build a similarity matrix (percentage of participants who put each pair together), read clusters from it and a dendrogram, and list cards with no clear home (placed in many groups) as candidates for cross-linking or renaming. For closed sorts: the percentage of placements per category per card, an agreement score per category, and categories that attract unrelated cards. Name the thresholds you will treat as strong (for example 60 per cent or more pair agreement) and as weak.
6. **From results to navigation.** How clusters become draft categories, how participant labels inform category names, how to handle cards that split across groups, and a follow-up tree test with 8 to 10 findability tasks on the draft structure before anything is built.
</task>

<constraints>
- Use only content from the inventory. Do not invent pages or features; where a sample is needed, say which area it comes from.
- Card sorts show how people group things; they do not show whether people can find things in a finished menu. Say so, and keep the tree test in the plan.
- Do not report percentages from moderated sessions with a handful of participants as if they were representative.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Study type
Recommendation and reason in 2 to 4 sentences.
## Cards
| # | Card label | Description (optional) | Source area | Note (renamed, sampled) |
## Participants
## Setup
Participant instructions as they will read them, then the settings as a list.
## Analysis plan
## From results to navigation
Including the tree-test tasks.
## Risks
</output_format>
