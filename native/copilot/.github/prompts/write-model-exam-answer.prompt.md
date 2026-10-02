---
description: Writes a model answer to a past exam question annotated against the mark scheme, showing where each mark is earned and how a weaker answer loses it. For students learning what examiners reward.
agent: agent
argument-hint: question mark_scheme marks level
---

# Write an annotated model exam answer

<context>
Students who know the content still lose marks because they do not know what a mark looks like: the command word asked for analysis and they described, the mark scheme wanted a unit and a stated assumption, the top level needed a supported judgement. An annotated model answer shows exactly where each mark is earned, and comparing it with weaker versions shows how marks slip away.
</context>

<task>
Write an annotated model answer to this past exam questionOnly if level was provided (leave it empty to skip):  for ${input:level:Optional qualification and level, e.g. "A-level Economics", "IB Biology HL", "AP US History", "first-year law".}Only if marks was provided (leave it empty to skip): , worth ${input:marks:Optional marks available, e.g. "6", "15 (AO1 5, AO2 10)".} marks.

<question>
${input:question:The past exam question exactly as set, including any source extract, data or diagram described in words.}
</question>
Only if mark_scheme was provided (leave it empty to skip): 
<mark_scheme>
${input:mark_scheme:Optional official mark scheme or level descriptors for the question. Without it the marking is reconstructed and labelled as such.}
</mark_scheme>

1. **What the question wants.** Name the command word and what it requires, the content area, any constraint (number of points, a named case, "using the data"), and how marks are awarded. If no mark scheme was given, reconstruct the likely marking from the level and marks (point-based marks, method and accuracy marks, or level descriptors with assessment objectives) and label it clearly as reconstructed, not official.
2. **Model answer.** Write a full-marks answer that a strong candidate could produce in the exam's time, proportionate to the marks: no padding, nothing beyond the level. Check every fact, figure and calculation; show working and units for quantitative questions.
3. **Annotate.** Mark each place a mark is earned with a bracketed tag in the answer, such as [M1] [A1] for method and accuracy, [1] for a point mark, or [AO2] for an assessment objective, and explain each tag in a table below.
4. **How weaker answers lose marks.** Write short excerpts of two weaker answers, a typical middle answer and a typical low one, using the mistakes examiners commonly report for this kind of question (describing instead of explaining, unsupported judgement, a missing unit, generic points not tied to the source). For each, say what it would score and why.
5. **Transferable lessons.** 3 to 5 rules that apply to other questions with this command word or format.
</task>

<constraints>
- When a mark scheme is given, follow it exactly; do not award marks it does not allow or add requirements it does not have.
- Never claim the reconstructed marking is official or quote examiner reports you have not been given.
- If the question looks like live coursework or an exam currently in progress rather than a past paper, say you can help the student plan their own answer instead, and stop.
- If the question depends on a source, diagram or data that is missing, ask for it.
</constraints>

<output_format>
Use the section headings from the output contract. The model answer in plain paragraphs (or numbered working for calculations) with inline mark tags. "Where the marks are" as a table: Tag | What earned it. Weaker answers as quoted excerpts, each followed by "Likely mark:" and two or three bullets.
</output_format>
