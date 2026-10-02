<context>
Video models read a prompt as a description of one continuous shot. They do best with one clear subject, one main action described with a precise verb, a specified camera behaviour, and a defined look. They struggle with several simultaneous complex actions, crowds interacting, fast hand movements, legible text, cause-and-effect physics and keeping a character identical across separate generations. Clips are short (often 5 to 10 seconds per generation, depending on the tool), so longer pieces are built from shots, and consistency comes from repeating the exact same descriptions of characters, wardrobe, setting and style in every shot and, where the tool supports it, from reference images or image-to-video starting frames. Some current tools also generate synchronised audio (dialogue, effects, ambience) from the prompt.
</context>

<task>
Write a video-generation prompt for this idea.

<idea>
[IDEA]
</idea>

Target tool: generic
Total duration: 8 seconds

1. **Interpretation:** two or three lines on the video you are aiming for, the choices you made where the idea was open, and whether it fits in one shot. If the idea is too open to film (for example "something epic for my brand"), ask up to three questions (subject, setting, purpose or mood) and stop.
2. **Prompt** (one shot): write a single paragraph in this order, with concrete visual words:
   - **Shot and camera:** shot size, angle, lens feel, and one camera movement (static, slow push in, pull out, pan, tilt, tracking alongside, orbit, crane up, handheld), with its speed;
   - **Subject:** who or what, with fixed visual identifiers (age range, build, hair, clothing, colours);
   - **Action:** one main action with a precise verb and its pace, beginning to end within the shot;
   - **Setting:** place, time of day, weather, background activity kept simple;
   - **Light:** source, direction, quality and colour;
   - **Style:** live-action cinematic, documentary, animation style described by technique, film stock or grade, frame rate feel (slow motion, real time);
   - **Audio** (only for tools that generate sound): ambience, effects, and any short line of dialogue in quotes with who says it.
3. **Shot list:** if 8 seconds is longer than one generation in generic (assume about 5 to 10 seconds per shot if unsure, and say so), split it into shots in a table: shot number, duration, shot size and camera, action, transition (cut, match cut, continuous), and a full standalone prompt for each shot that repeats the consistency block. If one shot suffices, write "Single shot".
4. **Consistency block:** a reusable paragraph describing each recurring character, outfit, setting and visual style in fixed wording to paste into every shot; recommend generating a reference image first and using image-to-video or the tool's reference or character feature if it has one.
5. **Settings:** aspect ratio for the use (16:9 for widescreen, 9:16 for vertical social, 1:1 or 4:5 for feeds), duration per clip, and any settings the tool commonly offers (motion strength, seed reuse for consistency, resolution). Note that settings and limits change between versions and tell the user to check their tool's documentation.
6. **Variations:** two alternative prompts that change one decision each (camera, light or style) and what each changes.
7. **Troubleshooting:** three fixes specific to this video for common failures (subject morphing, too much or too little motion, the camera ignoring instructions, warped hands or faces, unwanted text).
</task>

<constraints>
- Keep each shot prompt focused: one subject focus, one main action, one camera movement. Move extra actions into separate shots.
- Do not ask the model to render readable text in the frame; add text in editing instead and say so.
- Do not write prompts that depict real, identifiable people (including public figures) doing or saying things they did not do, sexualised content of real people or any minors, or footage designed to pass as real news, evidence or a real brand's advertising.
- Do not imitate copyrighted characters or a living director's signature style by name; describe the visual qualities instead.
- Phrase prompts positively ("an empty street") rather than relying on negatives, unless the tool has a separate negative prompt field.
</constraints>

<output_format>
## Interpretation
## Prompt
In a code block, ready to paste.
## Shot list
Table, then one code block per shot; or "Single shot".
## Consistency block
In a code block.
## Settings
## Variations
## Troubleshooting
</output_format>
