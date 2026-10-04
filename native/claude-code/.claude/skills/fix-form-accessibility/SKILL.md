---
name: fix-form-accessibility
description: Builds or repairs a web form with programmatic labels, grouping, autocomplete, helpful error messages and announced validation. Use for sign-up, checkout, settings or any data-entry form.
license: CC0-1.0
arguments:
  - form
  - framework
argument-hint: <form> [framework]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: accessibility
  source: https://hermes-ide.com/prompts/fix-form-accessibility
  catalog: 2026.1004.2
---

# Build or fix an accessible form

## Inputs

- `form` (required): Existing form code to repair, or a spec of the fields, rules and submit behaviour to build from.
- `framework` (optional): UI framework and form library, if any, for example "React with react-hook-form". Leave empty for plain HTML.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Forms are where accessibility failures cost the most: a person who cannot complete sign-up or checkout leaves. The recurring faults are a placeholder used as the only label, radio buttons with no group label, errors shown only in red, errors that are not announced or not tied to their field, focus left on the submit button after a failed submit, a disabled submit button that never says why, and password or one-time-code fields that block paste.
</context>

<task>
Build or repair this form (framework: $framework; if empty, use plain HTML and minimal JavaScript):

$form

1. If you were given code, list its barriers first, each with its WCAG criterion. If you were given a spec, skip to building.
2. **Labels and structure:**
   - Every control has a visible `label` tied by `for` and `id`, or by wrapping. A placeholder is never the label.
   - Related radios, checkboxes and multi-part fields (date of birth, address) sit in a `fieldset` with a `legend`.
   - The label text matches the accessible name (2.5.3).
3. **Input purpose (1.3.5):** set `autocomplete` tokens for personal data (`name`, `given-name`, `email`, `tel`, `street-address`, `postal-code`, `cc-number`, `one-time-code`, `new-password`, `current-password`). Use the right `type` and `inputmode`: `type="email"` and `type="tel"`, and `inputmode="numeric"` instead of `type="number"` for codes and card numbers.
4. **Required fields and instructions:** use the native `required` attribute, plus a visible indicator that does not rely on colour alone. Tie format hints to their field with `aria-describedby`, and show them before the user types.
5. **Errors (3.3.1, 3.3.3):**
   - Validate on submit, and on blur only for a field that already has an error.
   - On a failed submit, either move focus to an error summary at the top that links to each field, or move focus to the first invalid field. Pick one and use it consistently.
   - Each field error is text that says how to fix it ("Enter a date like 21/04/1990"), is linked by `aria-describedby`, and sets `aria-invalid="true"`. Clear it as soon as the input becomes valid.
   - Announce async results (such as "username taken") through a polite live region that exists in the DOM before it changes.
6. **Do not** disable the submit button to signal invalid input. Do not block paste in password or code fields (3.3.8). Do not ask again for information already given in the same process (3.3.7). Keep targets at least 24 by 24 CSS pixels (2.5.8).
7. Keep the existing visual design and validation rules. Change only what accessibility requires, and say where it required a visible change.
</task>

<constraints>
- Native HTML first. Add ARIA only where HTML cannot express it.
- With a form library, use its own error and registration APIs rather than working around them.
- Do not invent validation rules the form or spec did not have. List any you think are missing in one line each.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Issues
| # | Problem | WCAG SC | Field or line | Fix |
Write "Built from spec" instead when no code was given.

## Code
The complete fixed or new form.

## Validation behaviour
Numbered: when validation runs, where focus goes, and what is announced.

## Test checklist
Keyboard-only and screen-reader checks for filling, failing, fixing and submitting the form.
</output_format>
