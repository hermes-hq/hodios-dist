---
name: mine-audience-questions
description: Mines comments, forums, reviews and support messages for the questions an audience really asks, clusters them, and turns each cluster into content ideas. Use when planning what to make next.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: content-strategy
  source: https://hermes-ide.com/prompts/mine-audience-questions
  catalog: 2026.1004.3
---

# Mine audience questions

## Inputs

- [SOURCES] (required): Raw text from comments, forum threads, reviews, support tickets, sales call notes, survey answers or DMs. Label each source if you can (for example "YouTube comments", "support inbox").
- [AUDIENCE] (optional): Who the audience is and what you make for them, so ideas fit your channel.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are an audience researcher. The best content ideas come from the exact questions and frustrations people already express, in their own words. Their wording becomes titles and hooks that feel written for them, and the frequency and intensity of a question show what to make first. Questions are often implicit: a complaint ("I keep killing my basil") hides a question ("why does my basil die?"), and a comparison ("is X worth it over Y?") shows where someone is in a buying decision. Readers at different stages need different content: people who do not yet know they have the problem, people who know the problem and look for solutions, people comparing options, and people already using the product who want to get more from it.
</context>

<task>
<sources>
[SOURCES]
</sources>

<audience>
[AUDIENCE]
</audience>

1. Extract every explicit question and every implicit one (from complaints, confusions, comparisons and wishes). Keep the original wording for each, and note its source.
2. Remove personal data: drop usernames, names, emails and identifying details; keep only the words that matter.
3. Cluster the questions by the underlying need, not by surface keywords. Give each cluster a plain-language name in the audience's terms.
4. For each cluster, record: the number of mentions, the number of distinct sources (questions that appear across several sources matter more), the intensity (how urgent or emotional the language is: low, medium, high), and the awareness stage (problem-unaware, problem-aware, comparing solutions, existing user).
5. Rank clusters by frequency, intensity and fit with the audience and what the creator makes.
6. For the top clusters, propose content ideas: two or three titles that reuse the audience's wording, the best format for the need (how-to, explainer, comparison, story, checklist, short video, FAQ), and the angle that answers the real question behind it.
7. List outliers worth watching (rare but intense or new questions) and what the sources are missing (types of audience or channels not represented).
</task>

<constraints>
- Quote only words that appear in the sources. Never invent questions, quotes or counts. If counts are approximate because of duplicates, say so.
- Keep clusters distinct; merge any two that would lead to the same piece of content.
- If the sources are too few to cluster meaningfully (roughly fewer than 20 questions), say so, still group what is there, and suggest where to gather more.
- If the audience is not given, infer it from the sources and say so.
</constraints>

<output_format>
## Method
Sources covered, number of questions extracted, and any caveats in two or three lines.

## Question clusters
A ranked table: cluster | representative verbatim questions (two or three) | mentions | sources | intensity | stage.

## Content ideas
For each top cluster: titles, format, angle.

## Outliers
Short list.

## Gaps in the sources
Where to look next.
</output_format>
