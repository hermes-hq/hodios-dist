<context>
A model card tells someone deciding whether to use a model what it is for, what it was trained and tested on, where it works and where it fails. Readers include engineers integrating it, reviewers approving its release and people affected by its decisions. Weak cards read like marketing: one headline metric, no slices, limitations that are generic or invented, and no out-of-scope uses. A useful card states only what the evidence supports and says plainly what was never measured.
</context>

<task>
Write a model card from these notes:
[MODEL_NOTES]

1. Fill each section from the evidence: model details (name, version, type, architecture or base model, date, owner, license), intended use and users, out-of-scope uses, training data (sources, size, time range, preprocessing, known gaps), evaluation data, metrics, limitations, ethical considerations, and recommendations for users.
2. Derive out-of-scope uses from the evidence. For example, training data in one language makes other languages out of scope, and data from one period makes later periods unverified.
3. Report metrics overall and by every slice available, with sample sizes and confidence intervals where they exist. Call out the largest gap between slices with its numbers.
4. Where the notes say nothing, write "Not documented" and add a precise question to Gaps to fill naming who or what could answer it.
5. Flag contradictions between the notes and the results, such as a claim of multilingual support with English-only evaluation.
</task>

<constraints>
- Never invent a number, dataset, license or limitation. Mark anything you inferred as an inference.
- Do not round or average away a disparity between slices.
- Write for a technical reader who is not on the team, in plain language, defining any metric name a reader may not know.
- Keep marketing language out ("state-of-the-art", "robust", "unbiased").
</constraints>

<output_format>
A Markdown model card with these headings, in order: Model details, Intended use, Out-of-scope uses, Training data, Evaluation data, Metrics, Limitations, Ethical considerations, Recommendations, Gaps to fill. Present metrics as a table: slice | metric | value | sample size. Gaps to fill is a numbered list of questions.
</output_format>
