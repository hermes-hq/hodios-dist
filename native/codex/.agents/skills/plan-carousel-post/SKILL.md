---
name: plan-carousel-post
description: Plans an Instagram or LinkedIn carousel slide by slide with a hook slide, one idea per slide, visual notes, a save-worthy payoff and the caption. Use when teaching something on social.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: social-media
  source: https://hermes-ide.com/prompts/plan-carousel-post
  catalog: 2026.1002.2
---

# Plan a carousel post

## Inputs

- [TOPIC] (required): What the carousel teaches or argues, who it is for, and any notes, steps, examples or data to include.
- [PLATFORM] (optional; one of: instagram, linkedin; default: linkedin): Where it will be posted. LinkedIn carousels are uploaded as a PDF document; Instagram carousels are image posts.
- [SLIDES] (optional; default: 8): Number of slides, including the cover and the final slide.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You design educational carousels for social media. A carousel is read in a feed, on a phone, with a thumb ready to scroll away. The cover slide has one job: make the right person swipe. Every following slide must give a reason to swipe again, with one idea per slide and few enough words to read in a couple of seconds. The final slides must deliver something worth saving or sharing (a checklist, a framework, a before and after, a summary), because saves and shares are the strongest signals that a post was useful. The format differs by platform: on LinkedIn a carousel is a PDF document post shown with page-turning, read by a professional audience; on Instagram it is a set of images, usually in a 4:5 portrait format, read by a broader audience in a more visual style.
</context>

<task>
<topic>
[TOPIC]
</topic>

Platform: [PLATFORM]. Slides: [SLIDES].

1. Choose the angle: who the carousel is for and the single promise of the cover slide. Offer three cover headline options (a specific outcome, a mistake to avoid, a contrarian or surprising claim) and pick one.
2. Plan the slides. Slide 1 is the cover. Slide 2 confirms the promise and tells the reader why it matters to them. The middle slides each carry one idea, in order, with a short headline and supporting text. The second-to-last slide delivers the payoff (the summary, checklist or framework someone would save). The last slide is the call to action, chosen for the goal (save, share with someone, comment with a specific answer, follow, or visit a link in profile).
3. For each slide give: the headline, the body text, a visual note (layout, icon, diagram, screenshot, photo), and alt text.
4. Write the caption for [PLATFORM]: a first line that works on its own before the "more" cut-off, two or three short paragraphs that add context rather than repeating the slides, the call to action, and a few relevant hashtags.
5. Give design notes for consistency: slide size, font sizes legible on a phone, contrast, a consistent layout, slide numbers or a progress cue, and the creator's handle or logo placement.
</task>

<constraints>
- Keep each slide to about 25 words or fewer, the cover to about 10.
- Use exactly [SLIDES] slides. If the topic needs more, split it into a series and say so; if it needs fewer, say which slides to drop. If [SLIDES] is above what the platform accepts (Instagram has allowed up to 20 images per carousel; check the current limit) or beyond what readers will swipe through (usually more than about 12), say so and propose a shorter version.
- Do not invent statistics, research, quotes or results. Where one would help, add `[STAT: …]` or `[EXAMPLE: …]` and list it under Fill before posting.
- No engagement bait ("comment YES if…") and no cover promise the slides do not deliver.
- Write in plain language suited to the platform: more professional and specific on LinkedIn, more visual and conversational on Instagram.
</constraints>

<output_format>
## Angle
Audience, promise, three cover options and the pick.

## Slides
One block per slide: `### Slide N: <role>` then Headline, Body, Visual, Alt text.

## Caption
Ready to paste.

## Design notes
A short list.

## Fill before posting
Every placeholder, plus what to check before publishing.
</output_format>
