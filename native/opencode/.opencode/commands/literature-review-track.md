---
description: Takes a literature review from research question and search strategy through screening, an extraction matrix and a written synthesis, with approval between steps. For students and researchers.
---

# Literature review track

## Inputs

- [RESEARCH_QUESTION] (required): The question the review should answer, however rough.
- [SLUG] (optional; default: literature-review): Short kebab-case name for the review, used for the folder the step artifacts are saved in.

Read each value from the arguments below. If a required value is missing, ask for it once.

Runs a literature review on "[RESEARCH_QUESTION]" the way a supervisor would expect it to be done: a protocol first, a reproducible search, transparent screening, a faithful extraction matrix, then a thematic synthesis. Each step writes one artifact and stops for approval, and later steps build on the approved artifacts instead of re-asking.

Rules for every step: work only from records and texts the user supplies or that you retrieved with a search tool in this session; never invent a paper, citation, DOI or count; say "not reported" or "not available" instead of guessing; and keep a running list of decisions so the review can be reported honestly (for example with PRISMA for systematic reviews).

## Steps

Work through these steps in order. Do not skip a gate.

1. question (plan)
2. search (discover)
3. screen (discover)
4. extract (discover)
5. synthesize (build)

### Step 1: Question and protocol

Turn "[RESEARCH_QUESTION]" into a review protocol the rest of the track can follow.

1. Ask, in one message, only what you need and cannot infer: the purpose (thesis chapter, article, grant, policy brief), the review type they need or can afford (narrative, scoping, systematic, rapid), the deadline, and any must-include sources or databases they have access to.
2. Restate the question with the framework that fits it: PICO or PECO for interventions and exposures, PEO or SPIDER for qualitative and mixed questions, PCC for scoping reviews. Show each element.
3. Write inclusion and exclusion criteria: population, intervention or phenomenon, comparator, outcomes, study designs, languages, publication years and publication types (for example peer-reviewed only, or including preprints and grey literature), each with a one-line reason.
4. List the main concepts the search must cover, and the outcome or themes the synthesis will report.

Write the protocol as Markdown with sections Question, Framework, Criteria, Concepts, Deliverable. Flag any criterion that will make the review too narrow (very few studies likely) or too broad (thousands of records).

Stop and wait for approval.

Save this step's result to `reviews/[SLUG]/01-protocol.md`.

**Gate:** stop here and wait for the user's approval before step 2 (search).

### Step 2: Search strategy

Using the approved protocol, design a search that someone else could rerun and get the same records.

1. For each concept, list synonyms, spelling variants, truncation (for example `adolescen*`) and the database's controlled vocabulary where one exists (MeSH for PubMed, Emtree for Embase, ERIC descriptors, APA Thesaurus terms). Say when you are unsure a subject heading exists and suggest checking it in the database's thesaurus.
2. Combine terms with OR inside a concept and AND across concepts, then write one search string per database the user can use, adapted to its syntax and field tags.
3. Add supplementary methods: backward and forward citation chasing from key papers, grey literature sources that fit the field, and trial or preprint registries where relevant.
4. If you have a web or literature search tool, run the strings, and record the date, the database and the number of results for each. If you do not, give the strings and ask the user to run them and paste back the exported records (titles, abstracts and citation details).

Write a search log as Markdown: a table of database | string | date run | results, followed by the supplementary methods.

Never list papers you did not retrieve in this session or receive from the user, and never estimate a result count you did not see.

Stop and wait for approval and for the records.

Save this step's result to `reviews/[SLUG]/02-search-log.md`.

**Gate:** stop here and wait for the user's approval before step 3 (screen).

### Step 3: Screening

Screen the records the user supplied against the approved criteria.

1. Remove duplicates (same title and first author, or same DOI) and count them.
2. Screen titles and abstracts. For each record give a decision, include, exclude or unsure, and for exclusions the single criterion that fails (for example "wrong population", "not empirical", "outside date range"). Treat "unsure" as include for full-text review; it is cheaper to read one more paper than to miss one.
3. For records the user then provides in full text, repeat the screening and give a reason for every full-text exclusion.
4. Count records at each stage: identified, duplicates removed, screened, excluded at title and abstract, full texts assessed, excluded with reasons, included.

Write the screening record as Markdown: a decisions table (ID | citation | decision | reason) and the counts laid out as a PRISMA-style flow in text. For a systematic review, remind the user that a second, independent screener on at least a sample of records is expected, and how to report agreement.

Stop and wait for approval and for the full texts of included studies.

Save this step's result to `reviews/[SLUG]/03-screening.md`.

**Gate:** stop here and wait for the user's approval before step 4 (extract).

### Step 4: Extraction and appraisal

Extract data from the included studies into one matrix.

1. Use these columns unless the protocol says otherwise: ID (first author + year), aim, design, setting and country, sample (size and who), exposure or intervention, comparator, outcomes and measures, key findings with numbers, limitations, funding.
2. Fill each cell from that study's text only. Copy numbers exactly. Write "NR" when a value is not reported and add "[inferred]" when you derived it rather than read it.
3. Appraise each study with a tool that fits its design and say which one you used, for example RoB 2 for randomised trials, ROBINS-I for non-randomised interventions, the CASP or JBI checklists for qualitative and observational studies, and MMAT for mixed methods. Give the overall judgement and the one or two domains that drive it.
4. Note anything that makes studies hard to compare (different measures, follow-up times or definitions).

Write the matrix and the appraisal table as Markdown, followed by extraction notes listing every NR, every inference and every judgement call.

Stop and wait for approval.

Save this step's result to `reviews/[SLUG]/04-matrix.md`.

**Gate:** stop here and wait for the user's approval before step 5 (synthesize).

### Step 5: Synthesis

Write the review's synthesis from the approved matrix and appraisal, answering "[RESEARCH_QUESTION]".

1. Group the findings into themes that answer the question, not one paragraph per study. For quantitative findings that cannot be pooled, use a structured narrative synthesis: group by outcome, report direction and size of effects, and give weight to the stronger designs and lower risk of bias.
2. For each theme, write a topic sentence that makes a claim, the evidence from several studies, and why studies agree or differ.
3. State how confident the evidence lets you be for each main finding (for example strong, moderate, limited, conflicting) and why, in the spirit of GRADE where it applies.
4. Close with the gaps the review exposes and the limitations of the review itself: databases searched, languages, single screener, date of search.
5. Cite only included studies, in the citation style the user asked for (APA if none), and add the reference list.

Write the synthesis as Markdown with a methods summary paragraph (search, screening counts, appraisal tools), the thematic findings, the gaps, the limitations and the references. Finish with a list of anything the user must check before submitting: missing citation details, claims resting on one study, and counts that need confirming.

Save this step's result to `reviews/[SLUG]/05-synthesis.md`.

Arguments: $ARGUMENTS
