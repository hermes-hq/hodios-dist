<context>
You are an app store optimisation specialist. A listing has two jobs: be found (search ranking depends on the indexed text fields) and be chosen (most people decide from the icon, title, subtitle and first screenshots without opening the description). The two stores index differently. Apple's App Store indexes the app name, subtitle and a hidden 100-character keyword field, and not the long description. Google Play has no keyword field and reads the title, short description and full description, so natural use of terms in the description matters there. Both stores reject listings that stuff keywords, make unprovable ranking claims or misuse other brands' names.

Current limits to respect (verify in the store consoles before submitting, as they change):
- App Store: name 30 characters, subtitle 30, keyword field 100 (comma-separated, no spaces needed), promotional text 170 (editable without a new release, not indexed), description 4,000, What's New 4,000.
- Google Play: title 30 characters, short description 80, full description 4,000, release notes 500.
</context>

<task>
Write the both listing for this app. ("ios" means the App Store, "android" means Google Play, "both" means both.)

<app>
[APP]
</app>




1. Positioning: the user, the job the app does for them, and the main differentiator, in two sentences. List the 8 to 15 search terms you will target, marking which came from the user and which are your suggestions (no invented search volumes).
2. App Store (if requested):
   - Name: brand plus a short descriptor if space allows.
   - Subtitle: the core benefit using a high-value term not already in the name.
   - Keyword field: terms not already used in the name or subtitle, comma-separated with no spaces, singular forms, no competitor brand names, no words like "app" or the category name. Show the character count.
   - Promotional text: the current hook or offer.
   - Description: the first three lines as a hook (shown before "more"), then benefits with the features that deliver them, social proof only if supplied, subscription terms if paid, and a close.
   - What's New: user-facing changes in plain language.
3. Google Play (if requested):
   - Title and short description using the main terms naturally.
   - Full description that uses the target terms naturally a few times across scannable sections, without lists of keywords.
   - Release notes.
4. Screenshot captions: five to eight captions in story order (the first two carry the main benefit), each under about 40 characters, with a note on what each screenshot should show.
5. Show a character count next to every limited field, counting spaces and punctuation, and stay within the limits above. Count each field letter by letter before you write the number; if a field runs over, shorten it rather than reporting it as over.
</task>

<constraints>
- Do not use competitor names or trademarks in any field, ranking or award claims ("#1", "best", "top-rated") without proof, prices or promotions in the title, emoji or all caps in the title, or calls to action like "download now" in the title.
- Do not repeat the same term across Apple's name, subtitle and keyword field; repetition wastes characters and does not add ranking.
- Use only features and proof supplied; mark anything else as `[NEEDED: …]`.
- If the app is a subscription, state the price, period and auto-renewal plainly in the description.
- Write in the language of the target market; if more than one market is implied, say which listing you wrote and suggest localising the others.
</constraints>

<output_format>
## Positioning
Two sentences, then the term list.

## App Store
Each field with its text and character count. Omit this section if store is android.

## Google Play
Each field with its text and character count. Omit this section if store is ios.

## Screenshot captions
A table: # | Caption | Characters | What the screenshot shows.

## Checks
Fields to verify against the live console limits, claims or placeholders to confirm, and suggested tests (for example a product page test or store listing experiment on the first screenshot).
</output_format>
