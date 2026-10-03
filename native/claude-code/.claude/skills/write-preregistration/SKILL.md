---
name: write-preregistration
description: Writes a study preregistration with hypotheses, design, sampling plan, variables, exclusion rules and a pre-specified analysis plan, flagging open choices. For OSF or AsPredicted users.
license: CC0-1.0
arguments:
  - study
  - hypotheses
  - template
argument-hint: <study> <hypotheses> [template]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: research-methods
  source: https://hermes-ide.com/prompts/write-preregistration
  catalog: 2026.1003.1
---

# Write a study preregistration

## Inputs

- `study` (required): The study design as you have it - question, design, participants, procedure, measures, planned analysis, sample size reasoning, and whether any data already exist.
- `hypotheses` (required): Your hypotheses or predictions, as precisely as you can state them, including direction.
- `template` (optional; one of: osf, aspredicted, secondary-data; default: osf): Which registration format to follow.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A preregistration is a time-stamped plan that separates confirmatory tests, decided before seeing the data, from exploratory analysis. It only protects against flexible analysis if it is specific enough that a stranger could run the analysis from it and reach the same decision: the exact variables and how they are computed, the statistical model, the inference criterion, the sample size and stopping rule, how outliers, missing data and exclusions are handled, and what result would count as support or as disconfirmation. Vague preregistrations ("we will use appropriate tests") give a false sense of rigour. The OSF Preregistration template covers study information, design, sampling, variables and the analysis plan; AsPredicted asks nine short questions; secondary-data templates add what the researchers already know about the dataset.
</context>

<task>
Write a $template preregistration for this study.
<study>
$study
</study>
<hypotheses>
$hypotheses
</hypotheses>

1. Rewrite each hypothesis so it is testable: name the variables, the direction, the population, and the specific statistical test that will evaluate it. Split compound hypotheses into separate ones and label each H1, H2, and so on.
2. Find every analysis choice the study description leaves open (for example the covariates, the outlier rule, the handling of missing data, one- or two-tailed tests, the correction for multiple comparisons, the smallest effect size of interest, manipulation checks) and list them first under Undecided choices with options and a recommended default. Draft the plan with your recommendation marked [CONFIRM].
3. Write the preregistration in the structure of the chosen template:
   - osf: study information (title, research questions, hypotheses); design plan (study type, blinding, design, randomisation); sampling plan (existing data, data collection procedures, sample size, sample size rationale, stopping rule); variables (manipulated, measured, indices); analysis plan (statistical models, transformations, inference criteria, data exclusion, missing data, exploratory analyses).
   - aspredicted: whether data have been collected, the main question or hypothesis, the key dependent variable and how it is measured, conditions, the analyses, outliers and exclusions, sample size, anything else, and the type of study.
   - secondary-data: the osf sections plus the dataset's source, what the authors have already seen or analysed in it, and how prior knowledge of the data could bias the plan.
4. For each hypothesis, state the decision rule: what result supports it, what result counts against it, and what result is inconclusive (for example an equivalence test against the smallest effect size of interest).
5. Separate confirmatory from exploratory analyses explicitly.
6. Add a deviations log template for reporting any departures from the plan.
</task>

<constraints>
- Do not invent a sample size, power, effect size or prior result. If the sample size rationale is missing, explain the options (a power analysis with a justified effect size, a precision target, resource constraints) and leave [SAMPLE SIZE RATIONALE] for the user.
- Every variable must have an operational definition: the instrument, items, scoring and the transformation.
- If data already exist or have been looked at, say so honestly in the plan and recommend the secondary-data template; a preregistration written after seeing the results is not a preregistration.
- Keep statistical terms precise. If a planned test does not match the design or the data type, say so and propose an appropriate one.
- Keep AsPredicted answers short, as the format requires; put detail in the osf template only.
</constraints>

<output_format>
## Undecided choices
Table: choice | options | recommended default | why.
## Preregistration
The template's sections in order, with [CONFIRM] markers on recommended choices.
## Deviations log
Empty table: date | planned | actual | reason | effect on conclusions.
</output_format>
