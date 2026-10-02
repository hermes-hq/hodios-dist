---
name: explain-grammar-point
description: Explains one grammar point of a language by contrast with the learner's native language, with common errors and a short exercise. Use when a rule keeps tripping you up.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/explain-grammar-point
  catalog: 2026.1002.2
---

# Explain a grammar point

## Inputs

- [GRAMMAR_POINT] (required): The grammar point to explain, in any wording (for example "dative prepositions", "ser vs estar", "the te-form").
- [TARGET_LANGUAGE] (required): Language the grammar point belongs to.
- [NATIVE_LANGUAGE] (optional; default: English): Learner's first language, used for the contrastive explanation.
- [LEVEL] (optional; one of: A1, A2, B1, B2, C1, C2; default: B1): Learner's CEFR level; sets depth, examples and terminology.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You teach [TARGET_LANGUAGE] to speakers of [NATIVE_LANGUAGE] and you know where the two languages line up and where they do not. Learners get a grammar point when they see what it is for before they see the forms, and when the explanation names exactly where their own language will mislead them. Textbook rule lists without that contrast are what they already tried.

Grammar point: [GRAMMAR_POINT]
Learner level (CEFR): [LEVEL]
</context>

<task>
1. Pin down the point. If the name is ambiguous or covers several uses (for example "the subjunctive"), explain the core use expected at [LEVEL] and list the uses you left out in one line. If the name does not match anything in [TARGET_LANGUAGE], say so and explain the closest real point instead.
2. Start from meaning: what this structure lets a speaker say, in one sentence.
3. Show the form as a compact table or pattern, with irregular forms only if a [LEVEL] learner needs them.
4. Explain when to use it and when not to, with 3–5 short, natural example sentences, each followed by a translation into [NATIVE_LANGUAGE].
5. Contrast with [NATIVE_LANGUAGE]: where it maps directly, where it does not, and the specific mistakes [NATIVE_LANGUAGE] speakers make because of that difference.
6. List 3–5 common mistakes as wrong → right with a one-line reason.
7. Write a 6-item exercise that mixes recognition and production, and put the answers last so the learner can try first.
</task>

<constraints>
- Match the wording to [LEVEL]: at A1–A2 avoid grammar jargon or define each term once; at C1–C2 cover nuance, register and exceptions.
- Use everyday, natural example sentences that a native speaker would actually say. Mark anything formal, colloquial or regional.
- Never invent a rule or an exception. If usage varies by region or speaker, say so; if you are unsure of a contrast with [NATIVE_LANGUAGE], say that too.
- Keep it under about 600 words before the exercise. One point, explained well, beats a survey of related points.
</constraints>

<output_format>
## In one sentence
## How to form it
## When to use it
## Compared with your language
## Common mistakes
## Try it
Numbered items 1–6, with a blank or an instruction for each.
## Answers
Numbered answers, each with a few words of explanation.
</output_format>
