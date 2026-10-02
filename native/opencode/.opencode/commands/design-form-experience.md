---
description: Designs a form's UX by cutting questions, ordering them, choosing input types, inline validation, error messages and progress for multi-step forms. Use for checkout, signup and application forms.
---

# Design a form experience

## Inputs

- [FORM_PURPOSE] (required): What the form is for, who fills it in, on which devices, what happens after submission, and known problems (drop-off, errors, support tickets).
- [FIELDS] (required): The current or proposed fields in order, with whether each is required and why the business wants it. Include any validation rules you already have.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
Forms are where products lose people. Common causes: asking for data nobody uses, splitting a name into three fields, placeholder text used as labels that vanish on typing, validation that shouts while the user is still typing, error messages like "Invalid input", password rules revealed only after failure, and multi-step forms with no idea how long they are. The best form improvement is usually a question removed, then a question made easier to answer.
</context>

<task>
Design the experience for this form.

<form_purpose>
[FORM_PURPOSE]
</form_purpose>

<fields>
[FIELDS]
</fields>

If the purpose or the fields are missing (for example "a signup form" with no field list), ask for them and stop.

1. **Question audit.** For every field ask: who uses this answer, for what, is it needed now or could it be asked later, can it be inferred (postcode lookup, card type from number, country from locale), and is it required or optional? Recommend keep, make optional, defer, infer or remove, with the reason. Flag fields that may be legally required (tax ids, age checks) and fields with personal or sensitive data (date of birth, gender, health) that need a clear purpose and data-minimisation review. When the business reason is not given, mark the field "reason needed" instead of guessing.
2. **Structure and order.** Order questions as a conversation: easy and familiar first, grouped by topic, sensitive ones later with an explanation of why they are asked. Decide one page or several steps: use steps when the form is long or branches, with one topic per step. Use a single column. Show conditional questions only when they apply.
3. **Field specification.** For each remaining field: label (visible, above the field, plain words), input type and control (text, email, tel, number only for real numbers, date pattern, radio buttons for up to about 5 options, select or search for long lists, checkbox, toggle only for instant settings), field width matched to the expected answer, autocomplete and keyboard hint for mobile, hint text where people need it (format, why we ask), optional marking ("(optional)" rather than asterisks everywhere), and default values only when safe.
4. **Validation and errors.** Validate on leaving a field (not on every keystroke) and again on submit; remove an error as soon as it is fixed. Accept reasonable formats (spaces in card numbers, different phone formats) instead of rejecting them. For each field, write the error messages for each failure: what went wrong and how to fix it, in plain language, without blame ("Enter a date of birth in the past" rather than "Invalid date"). On submit with errors, show an error summary at the top that links to each field and move focus to it. Show password requirements up front.
5. **Progress and submission.** For multi-step: step names and count, saving progress, back without losing data, and a review step before submitting anything binding. The submit button names the outcome ("Pay £42.00", "Create account"). Prevent double submission. Describe the success state and what happens next, and the failure state if the server rejects the submission.
6. **Accessibility.** Programmatic labels, grouped radio buttons and checkboxes with a legend, errors announced to screen readers and associated with fields, no information by colour alone, touch targets of at least 44 by 44 points, no time limits without a way to extend.
7. **Measure.** The metrics to watch (completion rate, time to complete, error rate per field, drop-off per step) and one or two A/B tests worth running.
</task>

<constraints>
- Do not invent business, legal or technical requirements. When a field's reason or rule is unknown, say what to confirm.
- No dark patterns: no pre-ticked marketing consent, no hidden costs revealed at the end, no fake urgency.
- Keep recommendations specific to this form; skip generic advice that does not change a field.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Question audit
| Field | Who uses it and why | Recommendation | Reason |
## Structure and order
Steps or sections with their fields, in order.
## Field specification
| Field | Label | Control and input type | Autocomplete / keyboard | Hint text | Required |
## Validation and errors
| Field | Rule | Error message |
Then the error summary behaviour.
## Progress and submission
## Accessibility
## Measure
</output_format>

Arguments: $ARGUMENTS
