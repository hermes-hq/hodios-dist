---
name: check-health-claim
description: Checks a health or nutrition claim against the hierarchy of evidence and explains in plain words what the research does and does not show, without personal medical advice. For health news readers.
license: CC0-1.0
metadata:
  version: 1.1.0
  kind: prompt
  category: fact-checking
  source: https://hermes-ide.com/prompts/check-health-claim
  catalog: 2026.1004.0
---

# Check a health or nutrition claim

## Inputs

- [CLAIM] (required): The claim in the words you saw it, for example "Turmeric works as well as ibuprofen for joint pain" or "Seed oils cause inflammation".
- [SOURCE] (optional): Where you saw it - the article, post, video or advert, with a link or the text, and any study it cites.
- [COUNTRY] (optional): Your country, so the answer points to your national health service, medicines regulator and guidelines, which differ between countries. Leave empty for international sources.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Health claims often rest on a real study that shows much less than the headline. The strength of evidence depends on the kind of study: systematic reviews and meta-analyses of randomised trials sit at the top, then individual randomised trials, then observational studies (which show associations that may be due to confounding), then case reports, laboratory and animal studies, and expert opinion. Common distortions are presenting an association as cause, an animal or cell result as a human one, a relative risk without the absolute risk, a surrogate marker (such as a blood test) as a health outcome, a tiny or short study as definitive, and evidence funded or promoted by someone selling the product. Readers need a clear answer about what is known, without being told what to do with their own health.
</context>

<task>
Check this health claim.
<claim>
[CLAIM]
</claim>
Only if [SOURCE] was provided: 
<source>
[SOURCE]
</source>
Only if [COUNTRY] was provided: Reader's country: [COUNTRY]. Prefer this country's national health service, medicines regulator and guidelines, and say where they differ from international guidance.

First decide your mode, and say which one at the top of the Short answer:
- **Checked against sources:** you can search the web and open pages in this session.
- **Provisional, from background knowledge:** you cannot. You may still explain what the established evidence broadly shows for well-studied questions, but you name no specific study, figure, guideline or URL, mark the verdict "provisional", and list the searches that would confirm it. For new, niche or fast-moving claims, give no verdict at all; explain what evidence would settle it and where to look.

1. **What the claim says:** restate it precisely: who it applies to, what effect on which outcome, how large, and whether it implies cause. If the claim is too vague to check (for example "seed oils are bad"), name the two or three specific claims it could mean and check the most common one, saying so.
2. **What the evidence shows:** look for the best available evidence, starting at the top of the hierarchy: systematic reviews (for example Cochrane), clinical guidelines from national health bodies, then large randomised trials, then observational studies. If the source cites a study, find and read it. For each piece of evidence, give the study type, population, size, outcome and result, using absolute numbers where available ("from 4 in 100 to 3 in 100"). In provisional mode, describe the kind and consistency of the evidence instead ("several small trials with mixed results").
3. **Why the claim may be misleading:** name each distortion you find (association presented as cause, animal or lab study, relative risk only, surrogate outcome, small or short study, cherry-picked study, conflict of interest, outdated evidence) and explain it in one or two plain sentences.
4. **Verdict:** supported, partly supported, not supported by good evidence, contradicted by good evidence, or too early to say. Say how certain the evidence is and why.
5. **What this means for you:** general context only: who should be cautious, possible harms or interactions the evidence mentions, and when the question is worth raising with a doctor or pharmacist.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Cite only sources you opened in this session, with links and dates. Never cite a study, guideline or statistic from memory, and never construct a URL.
- Prefer the most recent high-quality evidence, and say when guidance differs between countries or has changed.
- Do not tell the person to start, stop or change any medicine, supplement, diet or treatment. If the claim encourages stopping a prescribed treatment or delaying care, say in the Short answer, in either mode, that they should not change anything before talking to their doctor.
- Be fair: if a claim is partly true, say which part, and do not dismiss it just because it is unfashionable or promoted commercially.
- Write for a non-specialist; explain any term like "confidence interval" or "placebo-controlled" in a few words.
</constraints>

<output_format>
## Short answer
The mode, the verdict in bold (with "provisional" if it is), two sentences, and one line saying this is general information, not advice for their own health.
## What the claim says
## What the evidence shows
Table: source (linked) | study type | who and how many | result. In provisional mode, a short paragraph instead, with no named studies or figures.
## Why the claim may be misleading
Bullets.
## What this means for you
Short paragraph, with when to ask a doctor or pharmacist.
## Sources
Numbered list with links and dates, or, in provisional mode, the searches to run and where (for example the Cochrane Library, the national health service, the medicines regulator).
</output_format>
