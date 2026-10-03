---
name: build-series-bible
description: Compiles a series bible from drafts or notes (characters, places, world rules, timeline, terminology, open threads), citing sources and flagging every contradiction. Use for novel series and TV.
license: CC0-1.0
arguments:
  - drafts_or_notes
argument-hint: <drafts_or_notes>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: worldbuilding
  source: https://hermes-ide.com/prompts/build-series-bible
  catalog: 2026.1003.0
---

# Build a series bible

## Inputs

- `drafts_or_notes` (required): The manuscript chapters, scripts, outlines or notes to compile from. Label each source (e.g. "Book 1, ch. 3", "Ep 102", "notes.md") so entries can cite where facts come from.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A series bible is the single source of truth for a long story: who everyone is, how they look and speak, where things are, how the world works, what happened when, what things are called and which threads are still open. Writers and writers' rooms rely on it to avoid the errors readers notice: eye colours that change, a character who knows something too early, a magic rule broken, a name spelled three ways. A bible is only useful if it is accurate, so every entry must come from the text and point back to where it came from, and contradictions must be surfaced rather than silently resolved.
</context>

<task>
Compile a series bible from this material:

<material>
$drafts_or_notes
</material>

1. **Scope:** list the sources you received and their labels. If sources are unlabelled, label them yourself in order (Source 1, Source 2) and say so. If the material looks truncated or too long to cover fully, say which parts you covered.
2. **Overview:** the premise in two or three sentences, genre and tone, point of view and tense conventions, and the format (books, episodes) as the material shows them.
3. **Characters:** a table for main characters (name and aliases or nicknames; role; age or birth date; physical description; relationships; voice and verbal habits; what they want; what they know and when they learned it, if it matters; status at the latest point in the material; first appearance). Minor characters in a shorter list with one line each.
4. **Places:** each location with description, its geography relative to others, who lives or works there, and notable features, with sources.
5. **World rules:** how magic, technology, institutions, laws, religion or the economy work, as stated in the text, with limits and costs; include rules implied by events and mark them "inferred".
6. **Timeline:** events in chronological story order (not reading order) with dates or relative timing, and source for each; note flashbacks and time skips.
7. **Terminology:** a glossary of invented words, titles, ranks, slang and proper nouns, with the canonical spelling and capitalisation; list variant spellings found.
8. **Objects and recurring elements:** important objects (who has them where), running jokes, motifs and rituals.
9. **Open threads:** setups not yet paid off, unanswered questions, promises made to the reader, and characters left in suspense, each with where it was set up.
10. **Contradictions:** every inconsistency found, each with both (or all) versions quoted with their sources, the type (physical description, timeline, name or spelling, world rule, knowledge, location), and a note on which version appears more often or later. Do not pick the canonical version for the author unless one is clearly a typo.
11. **Unknowns:** important facts the material never establishes that the author may want to decide (a character's age, a city's distance from the capital).
</task>

<constraints>
- Use only what is in the material. Never invent details to fill an entry; leave the field blank or write "not stated". Mark anything inferred as "inferred" with the reasoning.
- Cite a source label for every fact in Characters, Places, World rules, Timeline and Contradictions.
- Quote exactly when listing contradictions and variant spellings.
- Keep entries short and scannable; this is a reference document, not a summary.
- Do not change the author's text or suggest plot changes; at most, note in Open threads where a payoff seems to be missing.
</constraints>

<output_format>
Use the sections in order as level-two headings. Characters, Terminology and Contradictions are tables. Put sources in square brackets, e.g. [Book 1, ch. 3].
</output_format>
