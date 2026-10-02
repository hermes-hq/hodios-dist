---
name: explain-historical-event
description: Explains a historical event through long and short-term causes, actors and motives, consequences and historians' debates, with a timeline and source-analysis questions. For history students.
license: CC0-1.0
arguments:
  - event
  - level
  - exam_board_or_focus
argument-hint: <event> [level] [exam_board_or_focus]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: tutoring
  source: https://hermes-ide.com/prompts/explain-historical-event
  catalog: 2026.1002.2
---

# Explain a historical event

## Inputs

- `event` (required): The event, process or turning point, e.g. "the outbreak of the First World War", "the Meiji Restoration", "the Montgomery bus boycott".
- `level` (optional; one of: school, university, general; default: school): school is secondary or high school; university adds historiographical depth; general is for curious readers with no exam in mind.
- `exam_board_or_focus` (optional): Optional exam board, unit or angle, e.g. "Edexcel GCSE Weimar and Nazi Germany", "AP US History period 5", "economic causes".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
History students lose marks less often for missing facts than for flat explanation: a list of causes with no sense of which mattered most, how they interacted, or why historians still argue. A good explanation separates long-term conditions from short-term triggers, shows people making choices under constraints, and treats interpretations as arguments built on evidence.
</context>

<task>
Explain $event for a $level audienceOnly if exam_board_or_focus was provided: , focused on $exam_board_or_focus.

1. **In brief:** what happened, where, when and why it matters, in 3 or 4 sentences.
2. **Timeline:** 8 to 15 dated entries from the earliest relevant background to the immediate aftermath. Check every date; if a date is uncertain or disputed, say so rather than picking one.
3. **Causes:** group them into long-term conditions (structural: economic, political, social, ideological, international) and short-term causes and triggers. For each, explain the mechanism (how it made the event more likely), not just its name. Then say how the causes interacted and which are usually considered most important, and why.
4. **Actors and motives:** the key individuals and groups, what each wanted, what constrained them and what choices they made. Include groups often left out of the standard account where the evidence supports it.
5. **Consequences:** short-term and long-term, intended and unintended, and for whom.
6. **How historians disagree:** the main interpretations or schools of thought on this event, what each emphasises and the kind of evidence it relies on. Name historians only when you are confident of who argued what; otherwise describe the interpretation without a name. For level "school", keep this to two or three clear positions.
7. **Source questions:** describe 3 types of primary source a student might meet on this event (a speech, a cartoon, a diary, a government record), and for each give questions on content, provenance (who, when, why), purpose and audience, and usefulness for a specific enquiry. Name a real source only when you are confident it exists and is accurately described.
8. **Check your understanding:** 4 questions, from recall to a "how far do you agree" judgement question in the style of the levelOnly if exam_board_or_focus was provided:  and of $exam_board_or_focus.
</task>

<constraints>
- Keep established fact, mainstream interpretation and contested claims visibly separate.
- Never invent quotations, statistics, historians, book titles or sources. If you are unsure of a figure, give a range and say it is approximate.
- For events involving atrocities, colonialism or ongoing political disputes, be accurate and humane: describe what happened plainly, attribute perspectives, and do not present denial or fringe claims as a legitimate side of the debate.
- Match the level: plain language and short paragraphs for school and general; more on historiography, terms and debates for university.
- If the event is ambiguous (several events share the name), ask which one, or state which one you chose.
</constraints>

<output_format>
Use the section headings from the output contract. Timeline as a table: Date | Event. Causes as two subsections (Long-term, Short-term and triggers) followed by a short "How they connect" paragraph. Keep the whole explanation under about 1,200 words for school and general, 1,800 for university.
</output_format>
