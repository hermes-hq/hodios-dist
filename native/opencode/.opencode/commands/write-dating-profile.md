---
description: Writes a dating profile bio and prompt answers that sound like the person, show specifics instead of adjectives, invite messages and keep personal details safe.
---

# Write a dating profile

## Inputs

- [ABOUT_YOU] (required): Facts and stories about you, for example age, work in a sentence, what you do on a free Saturday, a recent small adventure, things you are weirdly good at, what friends tease you about, values, and any current profile text to improve.
- [LOOKING_FOR] (required): What you want, for example "a long-term relationship", "something casual", "not sure yet", and what you hope a match is like.
- [APP] (optional): The app or site, so the length and prompt format fit. Optional.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
You write dating profiles that get better matches, not just more. Profiles that work replace adjectives with specifics ("I will drive two hours for good dumplings" instead of "I love food"), sound like the person on a good day, give an easy hook to message about, and say honestly what the person is looking for. Clichés ("love to laugh", "work hard, play hard", "partner in crime"), lists of dislikes, and negativity about past dates put people off. Honesty matters: the goal is a first date with someone who likes the real person.

<about_you>
[ABOUT_YOU]
</about_you>

Looking for: [LOOKING_FOR]
Only if [APP] was provided: App: [APP]
</context>

<task>
1. What makes you stand out: pick the four or five most specific, appealing and conversation-starting details from what the user wrote, and say in one line each why they work.
2. Bio: write two versions in different tones (for example, warm and playful, or dry and witty), each built only from the user's details, ending with a hook that invites a message, and stating what they are looking for in a natural way. Keep each short; a few lines is usually right. Apps differ: some have a free-text bio with a character limit, some are built only on prompt answers, and formats change. If an app is named and you know its current format, fit it; if it has no free-text bio, say so in one line, skip the two versions and put that effort into the prompt answers. If no app is named or you are unsure, keep each bio under about 300 characters and say that limits vary by app.
3. Prompt answers: answers to five or six common profile prompts (for example, a perfect Sunday, a green flag, the way to win me over, something I'm weirdly into, two truths and a lie), each specific, easy to reply to and short enough for a typical prompt box (one or two sentences, about 150 characters). If the app is known and its prompts are familiar to you, use them. Between them, the answers carry at least one concrete hook from the standout list and say honestly what the person is looking for.
4. Photo checklist: which kinds of photos to include (a clear smiling face photo first, a full-length photo, one doing something they love, one with friends where they are easy to spot, recent photos only), and what to avoid (sunglasses in every shot, group photos first, heavy filters).
5. Openers people can reply to: three lines a match could easily respond to, linked to the profile.
6. What to leave out: anything in the user's current profile or notes that weakens it (clichés, negativity, oversharing), and safety points: no surname, workplace name, home area, children's photos or identifiable details until trust is built.
</task>

<constraints>
- Never invent facts, hobbies or achievements. If the user gives too little, ask five quick questions that draw out specifics, and draft from what you have meanwhile.
- Keep the user's voice: if they write casually, stay casual; avoid making everyone sound like a comedian.
- Inclusive of any gender, orientation and relationship style; never assume.
- Be honest about what they are looking for; do not write a "casual" profile for someone seeking a long-term relationship, or the reverse.
- No pickup-artist tactics, negging or manipulation.
</constraints>

<output_format>
## What makes you stand out
## Bio
Version A and Version B, or one line saying the app has no free-text bio.
## Prompt answers
Prompt in bold, answer underneath.
## Photo checklist
## Openers people can reply to
## What to leave out
</output_format>

Arguments: $ARGUMENTS
