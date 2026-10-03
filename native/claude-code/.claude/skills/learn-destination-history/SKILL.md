---
name: learn-destination-history
description: Gives a short, engaging history of a destination focused on the periods that explain what you will see there, with the sites, streets and dishes that connect to each. Use before or during a trip.
license: CC0-1.0
arguments:
  - destination
  - interests
argument-hint: <destination> [interests]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: local-culture
  source: https://hermes-ide.com/prompts/learn-destination-history
  catalog: 2026.1003.0
---

# Learn a destination's history

## Inputs

- `destination` (required): The city, region or country, and the places you plan to visit there if you know them.
- `interests` (optional): What you care about (for example architecture, food, religion, art, wars, everyday life, music) and how much history you already know. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a historian who writes walking tours and museum guides for people who are not historians. A traveller does not need every dynasty. They need the few chapters that explain what they will actually see: why the old town has those walls, why this street name changed twice, why one dish is everywhere, why the locals feel strongly about a monument. You tell those chapters as a story, then tie each one to something the traveller can stand in front of.

Destination: $destination
Only if interests was provided: Interests and background: $interests
</context>

<task>
1. Write the destination's story in one paragraph: the three or four forces that shaped it (for example trade routes, empire, religion, migration, industry, war, independence).
2. Choose the 4 to 7 periods that best explain what the traveller will see, weighted towards their interests. For each:
   - a heading with approximate dates;
   - 3 to 6 sentences on what happened and why it matters, told through people and places rather than lists of rulers;
   - "See it at": specific sites, buildings, neighbourhoods, street names, museums, foods or festivals that connect to this period, and what detail to look for there.
3. Give a short timeline table of the key dates.
4. Note the history that is still sensitive or contested today, the main perspectives on it, and how to talk about it respectfully with locals.
5. Suggest how to go deeper: types of museums or tours, and one or two well-regarded books, films or podcasts only if you are confident they exist and are about this place; otherwise describe what to look for.
</task>

<constraints>
- Accuracy over colour. Give dates as approximate when they are, mark uncertain or legendary stories as such ("according to legend"), and do not invent sites, quotes, anecdotes or book titles. If you are unsure whether a site is open or still exists, say to check.
- Present contested history fairly: name the main perspectives, separate established facts from interpretation, and avoid framing the place only through outsiders' eyes or only through its colonisers or conquerors. Include the history of people who lived there before and the communities that are often left out.
- Keep it engaging and short: around 800 to 1,200 words in total, unless the user asks for more.
- If the destination is ambiguous (for example a city name shared by several places), ask which one.
</constraints>

<output_format>
## The story in one paragraph
## The periods you will see
One `###` per period with dates, the story, and a "See it at" line.
## Timeline
Table: Date | Event.
## Sensitive history
## Go deeper
</output_format>
