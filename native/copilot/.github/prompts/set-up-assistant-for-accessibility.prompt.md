---
description: Sets up an AI assistant for accessibility needs such as screen readers, dyslexia, low vision, ADHD or limited hand use, with custom instructions for output, settings to check and tests.
agent: agent
argument-hint: needs tools
---

# Set up an assistant for accessibility needs

<context>
Default assistant output is built for sighted mouse users who skim: wide Markdown tables, ASCII diagrams, emoji bullets, bold everywhere, long paragraphs, "click the blue button", and links labelled "here". For a screen-reader user, a table can read as a stream of pipes and dashes; for someone with dyslexia, dense paragraphs and italics slow everything down; for someone dictating by voice, long replies and options that need precise selection are tiring. Custom instructions can change most of this, and the person's own description of their needs is the best guide: needs vary widely within any label.

<needs>
${input:needs:What makes using an assistant harder for you or the person you are setting it up for, in your own words, for example "I use a screen reader and tables are a nightmare", "dyslexia, long paragraphs lose me", "I dictate everything".}
</needs>
Only if tools was provided (leave it empty to skip): 
<tools>
${input:tools:Optional: the assistant app and device used, and any assistive technology (screen reader, magnifier, voice control, text-to-speech, switch access).}
</tools>
</context>

<task>
1. Restate the needs as specific output problems to solve, in the person's terms. If the needs are too general to act on, ask up to three questions about what currently goes wrong and stop.
2. Write custom instructions that address each problem with concrete rules. Draw from what applies:
   - Screen reader: no ASCII art or box diagrams; tables only when asked and small, otherwise lists with labels; describe images and charts in words; headings for structure; descriptive link text; no reliance on colour or position ("the button on the left"); emoji used rarely and never as bullets.
   - Dyslexia or reading fatigue: short sentences and paragraphs, the main point first, plain words, lists for steps, no italics or long runs of capitals, a short summary at the top of long answers.
   - Low vision: short chunks, clear headings, no instructions that depend on seeing small visual details, offering text descriptions of screenshots.
   - Attention or memory: one step at a time when giving instructions, checklists, a recap of where we are on long tasks.
   - Limited hand use or voice input: brief replies by default, numbered options to choose by saying a number, tolerance for dictation errors without commenting on them.
   - Hearing: text alternatives for anything audio, captions or transcripts suggested for media.
3. List settings to check, generically because menus differ: text size and contrast, read-aloud or voice mode, dictation, keyboard shortcuts, compatibility with the person's assistive technology, and turning off auto-playing media.
4. Suggest habits that help: phrases the person can use mid-conversation to adjust ("shorter", "as a list", "describe the image").
5. Write five test prompts that would expose the old problems, with what good output looks like after the change.
</task>

<constraints>
- Follow the person's own description; do not assume needs from a diagnosis label or add rules for needs they did not mention.
- Respectful, practical tone. No pity, no medical advice.
- Do not claim exact menu names or features of a specific app as current fact.
- Keep the custom instructions under about 1,200 characters so they fit common limits, and say to check the tool's limit.
- Write this answer itself in the accessible form the person needs: if they use a screen reader, avoid tables in this reply too.
</constraints>

<output_format>
## What changes
Short list: problem, then the rule that fixes it.
## Custom instructions
One fenced block, ready to paste.
## Settings to check
## Habits that help
## Test prompts
Numbered list: prompt, then what good output looks like.
</output_format>
