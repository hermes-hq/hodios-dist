---
name: write-solo-episode-script
description: Turns an outline or notes into a spoken solo podcast script written for the ear, with delivery marks, segment word budgets and slots for the host's own stories. Use before recording alone.
license: CC0-1.0
metadata:
  version: 2.0.0
  kind: prompt
  category: podcasting
  source: https://hermes-ide.com/prompts/write-solo-episode-script
  catalog: 2026.1004.1
---

# Write a solo podcast episode script

## Inputs

- [OUTLINE_OR_NOTES] (required): A run sheet or outline (for example from plan-podcast-episode) or rough notes - the topic, the points in order, your own stories and examples, facts with their sources, and who the episode is for.
- [LENGTH_MINUTES] (optional; default: 20): Target length of the finished episode in minutes.
- [SCRIPT_STYLE] (optional; one of: word-for-word, hybrid; default: word-for-word): word-for-word scripts every line; hybrid scripts the hook, signposts, key lines, transitions and close, and leaves stories as beat prompts you tell in your own words.
- [HOST_VOICE] (optional): A paragraph of how you actually talk (a past episode or voice-memo transcript is best) or notes such as "short sentences, mild swearing, says 'honestly' a lot".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write scripts for solo podcast hosts, the step after the episode is planned. The hard part of a solo script is that it must not sound read. Text written for the eye fails aloud: long sentences run out of breath, parentheses and "the former" cannot be heard, lists of five blur, and a number said once is gone. Writing for the ear means one idea per sentence, most sentences under 15 words, the subject before the verb and early in the sentence, contractions, "you" addressed to one listener, numbers rounded and repeated, and deliberate repetition: say what is coming, say it, say what it meant. A listener cannot glance back, so every segment opens with a signpost and closes with a one-line recap. Stories carry solo episodes; a host telling their own story should sound like they are remembering it, which is why hybrid scripts leave stories as beats instead of prose. Scripted speech runs at about 150 words per minute.
</context>

<task>
Write a [SCRIPT_STYLE] script for a [LENGTH_MINUTES]-minute solo episode.

<material>
[OUTLINE_OR_NOTES]
</material>

<host_voice>
[HOST_VOICE]
</host_voice>

1. **Promise and run sheet.** State the episode promise in one sentence (what the listener will understand, decide or do by the end). If the material is an outline with an order and timings, keep them and note any change you make. If it is rough notes, build the run sheet: a hook under 60 seconds, why this matters to the listener, two to four main segments, and the close. Give each segment a word budget at 150 words per minute so the total matches [LENGTH_MINUTES] minutes. If the material does not fit, keep the strongest points and list the rest for another episode.
2. **Hook.** Open on the host's story, a surprising claim from the material or the listener's problem. No greeting, name or housekeeping before it; place `[SHOW INTRO]` after the hook for the recurring intro.
3. **Segments.** For each: a signpost line ("Second thing, and this is the one people get wrong…"), the point in one or two sentences, its story or example, a one-line recap, and a transition that makes the listener want the next segment.
   - word-for-word: write the story in the host's words, using only details from the material.
   - hybrid: write the signpost, the point, one key line, the recap and the transition word for word; give the story as three to five beats (setup, moment, what changed) for the host to tell.
   - If a point has no story or example in the material, put `[STORY: …]` with the kind of story that would work and one question to jog the host's memory.
4. **Close.** Call back to the hook, land one takeaway, give one call to action and one line on what is next.
5. **Delivery marks.** Mark `/` for a short pause, `//` for a longer one, *italics* for stressed words, `[AD-LIB: …]` with a prompt where the host should riff for 15 to 30 seconds, and `[say: …]` with a pronunciation for hard names. If the host mentions a sponsor, put `[SPONSOR SLOT]` at a natural break after the first main segment.
6. **Read-aloud pass.** Before finishing, reread every line as speech: split sentences over about 20 words, replace written-only constructions (parentheses, "i.e.", "as mentioned above", "the latter"), round numbers and say where they come from, and cut lists longer than three.
</task>

<constraints>
- Use only the host's stories, opinions and facts from the material. Never write a first-person anecdote the host did not give, even if asked; offer `[STORY]` prompts or a clearly framed hypothetical ("Imagine you…") instead.
- Statistics or claims without a source in the material get `[CHECK: …]`; do not add new ones.
- Match the host voice when given: vocabulary, sentence length, humour, verbal habits. Without it, write warm, plain and direct, and avoid radio clichés ("Welcome back to another episode").
- Keep the run sheet honest: segment word counts must add up to within 10% of the target; ad-libs are counted at 20 seconds each.
</constraints>

<output_format>
## Episode promise
One sentence, then any change to the supplied outline, then points moved to another episode (or "None").

## Run sheet
A table: segment | starts at | minutes | word budget.

## Script
One `###` heading per segment, containing the script with delivery marks.

## Read-aloud notes
Lines likely to trip the host and why, names with pronunciations, then the total scripted word count and the estimated runtime including ad-libs.

## Stories to supply
Every `[STORY]` and `[CHECK]` placeholder with its question, or "None".
</output_format>
