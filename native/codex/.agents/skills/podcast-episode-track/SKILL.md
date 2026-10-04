---
name: podcast-episode-track
description: Takes a podcast episode from topic to research and guest prep, a run sheet, post-recording show notes and clips, and a promo plan, pausing between steps. Use for each episode.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: podcasting
  source: https://hermes-ide.com/prompts/podcast-episode-track
  catalog: 2026.1004.1
---

# Podcast episode track

## Inputs

- [SHOW] (required): The show's name, audience, usual length and format, and the tone it is known for.
- [EPISODE_TOPIC] (required): The episode's topic or angle, the guest or panellists if any, and any notes or sources you already have.
- [FORMAT] (optional; one of: solo, interview, panel; default: interview): solo is one host; interview is a host with one guest; panel is a moderator with several guests.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Produces one [FORMAT] episode of [SHOW] about "[EPISODE_TOPIC]" in four approved steps: research and guest prep, then a timed run sheet for the recording, then (after the episode is recorded) show notes and clip picks from the real transcript, then a promotion plan. Each step produces one artifact and stops for the host's approval or edits; later steps build on the approved versions and never re-open settled decisions without asking. Step 3 cannot start until the host supplies a transcript or timestamped notes of the actual recording, because show notes and clips must reflect what was said, not what was planned. The host owns every editorial decision; the assistant drafts, keeps steps consistent and marks anything it cannot confirm instead of inventing it. If the host asks to skip the approvals, confirm once that later steps will then build on unreviewed choices; if they agree, run the remaining pre-recording steps in one reply, state the choice made at each skipped gate, and still wait for the transcript before step 3.

## Steps

Work through these steps in order. Do not skip a gate.

1. research (plan)
2. run-sheet (plan)
3. show-notes (build)
4. promo (ship)

### Step 1: Research and guest prep

Prepare the [FORMAT] episode of [SHOW] about "[EPISODE_TOPIC]".

1. Ask the host, in one message, for anything not already given: the guest or panellists and how to reach their past interviews, writing or talks; the episode's target length and release date; what listeners should come away with; anything off limits; and any sponsor slots to fit.
2. When you have the answers, write:
   - **Episode promise:** one sentence a listener would hear in the episode description and want to press play.
   - **Angle:** what this episode adds that the guest's other interviews (or the host's past episodes) did not. If the host has not shared past material, list what to check so the episode does not repeat it.
   - **Research brief:** the key facts, context and terms the host must know, each marked as supplied by the host or to be verified. Do not state facts about a real person or organisation that were not supplied; list them as questions to confirm.
   - **Guest prep** (interview and panel): a short pre-interview email to the guest covering the audience, the angle, the length, recording date and setup (headphones, quiet room, wired connection, local backup recording if the platform supports it), what will be edited, and two or three questions to think about. For a panel, add who covers which area and where disagreement is welcome.
   - **Solo prep** (solo): the stories, examples or data the host needs to gather, since one voice must carry the whole episode.
   - **Risks:** sensitive topics, claims that need checking, and anything that could need a legal or factual review.

Stop and wait for the host to approve or edit the promise, angle and prep. Do not write the run sheet yet.

**Gate:** stop here and wait for the user's approval before step 2 (run-sheet).

### Step 2: Run sheet

Turn the approved promise and research into a run sheet for recording the [FORMAT] episode of [SHOW].

1. **Cold open plan:** what moment, question or line should open the episode. Since the best moment is often only known after recording, give a target ("aim to capture the guest's story about…") and a fallback the host can record separately.
2. **Segments:** a table with time | segment | purpose | talking points or questions | transition into the next segment. Order the conversation from easy and concrete to deeper and more reflective, and put the most valuable material before the halfway point.
   - interview: a question path with follow-ups that ask for specifics ("what happened next?", "what number did you see?"), and one question the guest probably has not been asked.
   - panel: name who each question goes to first, plan one point of genuine disagreement, and note how to bring in quieter panellists.
   - solo: a clear arc with the stories and examples placed where energy usually dips.
3. **Sponsor and housekeeping:** where reads go (not before the first real content) and how long they take.
4. **Producer notes:** levels check, room tone, a clap or marker for sync if recording on separate devices, a reminder to record locally where possible, and what to listen for live (vague answers to revisit, stories worth asking for again more concisely).
5. **Must-capture list:** the three or four things the episode fails without.

Keep the total within the show's usual length plus about 20% for editing. Stop and wait for approval. After approval, tell the host that step 3 needs the transcript or timestamped notes from the recording, and wait for them.

**Gate:** stop here and wait for the user's approval before step 3 (show-notes).

### Step 3: Show notes and clips

Write show notes and pick clips for the recorded episode of [SHOW] about "[EPISODE_TOPIC]".

1. If the host has not supplied a transcript or timestamped notes of the actual recording, ask for them and stop. Do not write show notes from the run sheet: the plan is not what was said.
2. Compare the recording with the approved run sheet. Note anything that changed the episode's real promise, and use what was actually said.
3. Write the show notes:
   - **Title options:** three, under about 70 characters, built on the episode's real strongest idea, each promising only what the episode delivers.
   - **Description:** two or three sentences for podcast apps, front-loading the payoff, since apps cut descriptions short.
   - **Chapters:** timestamps from the transcript, with plain, specific labels.
   - **Key takeaways:** three to five, in the speakers' terms.
   - **Resources mentioned:** every book, tool, person or link mentioned, with `[LINK NEEDED]` instead of any URL that was not supplied.
   - **Guest bio and links:** only what the guest or host supplied.
4. Pick three to five clips for social video or audiograms: timestamp in and out, the verbatim lines, why it works on its own without context, a suggested caption and the platform it suits. Prefer 20 to 60 second moments with a clear setup and payoff.
5. Flag edit notes: sections that dragged, repeated stories, audio problems the host mentioned, and any line that should be cut or checked before release (factual claims, names, anything said off the record).

Quotes must be verbatim; trim filler only with `...`. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 4 (promo).

### Step 4: Promo plan

Plan the promotion of the approved [FORMAT] episode of [SHOW] about "[EPISODE_TOPIC]", using the approved show notes and clips.

1. **Release-week schedule:** a table of day | channel | asset | copy | owner, from release day to about a week after. Use only the channels the host already uses or mentions; ask if none are known.
2. **Copy for each asset:** one short post per channel built on a clip or takeaway, written for that channel's norms, each pointing to where to listen. No invented listener numbers, rankings or reviews.
3. **Guest amplification:** a short, ready-to-send message to the guest with the release date, the link placeholder, two suggested posts in their voice they can edit, and the clip files they are featured in. Make sharing easy, never obligatory.
4. **Newsletter or community mention:** two or three sentences for the host's newsletter or community, if they have one.
5. **Later reuse:** which clips or takeaways could resurface in a month (a related news hook, a later episode, a best-of), so the episode keeps working.
6. **What to measure:** downloads or plays at 7 and 30 days compared with the show's usual episodes, follows or subscriptions gained, clip performance by channel, and listener replies. Compare like with like, since numbers differ between hosting providers.

End with a short checklist of everything to finalise before release: links, artwork, chapters, ad reads, transcript upload and the guest message.
