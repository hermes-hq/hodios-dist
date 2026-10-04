---
name: facilitate-group-brainstorm
description: Plans and scripts a group brainstorm - framed challenge, warm-up, silent ideation, building, clustering, voting and next steps - timed to the group and slot. For teams generating ideas together.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: brainstorming
  source: https://hermes-ide.com/prompts/facilitate-group-brainstorm
  catalog: 2026.1004.3
---

# Facilitate a group brainstorm

## Inputs

- [CHALLENGE] (required): What the group needs ideas for, why now, any constraints (budget, timeline, what is off the table) and who decides afterwards.
- [GROUP_SIZE] (optional; default: 6): Number of participants, including you. Between 3 and 30 works; larger groups are split into tables.
- [DURATION_MINUTES] (optional; default: 60): Length of the session in minutes. 20 to 240 works; 45 to 120 is ideal, and under 45 gets a compressed format.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Open-floor group brainstorming produces fewer and less varied ideas than people working alone first, because of anchoring on early ideas, waiting for a turn, and fear of judgement. Sessions that work separate generating from judging, start with silent individual ideation (brainwriting), then build on each other's ideas, and converge with a transparent method. You plan a session that a non-specialist can run from your script.

<challenge>
[CHALLENGE]
</challenge>
Group size: [GROUP_SIZE] people. Duration: [DURATION_MINUTES] minutes.
</context>

<task>
1. Frame the challenge as one to three "How might we …?" questions that are neither too broad ("improve the company") nor too narrow (a disguised single solution). Note the constraints and who decides after the session. If the challenge is too vague to frame or no one owns the decision, say what to clarify first and still give a draft framing.
2. Plan the session to fit exactly [DURATION_MINUTES] minutes, with about 10 percent buffer. Adapt to [GROUP_SIZE] people: for more than 8, split into tables of 4 to 6 with a reporter each; for under 4, use more individual rounds. If the duration is under 45 minutes, use the compressed format: a two-minute warm-up or none, the stretch prompt folded into the building round, clustering done by the facilitator while people read the wall, and voting kept. Over 90 minutes, add a break. Include:
   - opening: purpose, the question, the ground rules (quantity over quality, no judging yet, build on others, one idea per note), and the decision owner;
   - a short warm-up that loosens thinking and relates to the challenge;
   - silent ideation: individual writing, one idea per sticky note or card;
   - building: a brainwriting pass (6-3-5 style or round-robin of notes) where people extend others' ideas;
   - a stretch round with a prompt that forces new territory (an extreme constraint, the opposite, how another industry would solve it);
   - clustering: grouping into themes and naming them;
   - convergence: dot voting with a clear criterion (for example impact and feasibility), and a quick check for a bold idea that deserves rescue;
   - close: top ideas, owners for next steps, and how people will hear what happens.
3. Write the facilitator's script for each block: what to say word for word for instructions, timing, and what to do if energy drops, one person dominates, or ideas stay safe.
4. List materials for in-person and remote (whiteboard tool) versions.
5. After the session: how to write up the output within 24 hours and turn the top ideas into tests.
</task>

<constraints>
- Times must add up to [DURATION_MINUTES] minutes; show the running clock.
- If [GROUP_SIZE] is outside 3 to 30 or [DURATION_MINUTES] is outside 20 to 240, use the nearest bound and say so.
- No icebreakers that embarrass people or take more than five minutes.
- Do not generate the group's ideas for them in the plan; offer at most three example ideas to explain an instruction.
</constraints>

<output_format>
## Framed challenge
The How might we questions, constraints and decision owner.
## Session at a glance
A table: Clock | Block | Minutes | Format | Output.
## Facilitation script
One subsection per block with the words to say in quotation marks and tips for problems.
## Materials
Two short lists: in person and remote.
## After the session
Numbered steps.
</output_format>
