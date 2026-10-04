---
name: write-formal-letter
description: Writes a formal letter to a bank, council, school, supplier or official body in the layout and conventions of the chosen country, with a clear purpose, references and a specific request.
license: CC0-1.0
arguments:
  - purpose
  - recipient
  - country_convention
  - facts_and_references
argument-hint: <purpose> <recipient> [country_convention] [facts_and_references]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: business-writing
  source: https://hermes-ide.com/prompts/write-formal-letter
  catalog: 2026.1004.2
---

# Write a formal letter

## Inputs

- `purpose` (required): What the letter must achieve, for example "ask the council to fix a broken streetlight", "cancel my gym contract" or "request a payment plan from the supplier".
- `recipient` (required): Who receives it, as precisely as you know, such as the organisation, department, named person and title, and their address.
- `country_convention` (optional; one of: us, uk, de, fr, br, generic; default: generic): Layout and etiquette to follow. us, uk, de (DIN 5008), fr, br, or generic for a neutral international layout.
- `facts_and_references` (optional): Your name and address, account, customer or case numbers, dates, earlier letters, amounts and enclosures. Anything missing becomes a placeholder.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Official bodies, banks and suppliers process letters by reference number and by the request in the first paragraph. A formal letter works when the clerk who opens it can see in ten seconds who is writing, which file it concerns and what action is being asked for by when. Layout and etiquette signal care, and getting them wrong in another country (a comma after "Mit freundlichen Grüßen", "Yours sincerely" after "Dear Sir or Madam", a missing "Objet") makes the writer look careless.

Conventions to apply:
- **us:** block format; sender address (or letterhead), date as "October 3, 2026", inside address, optional "Re:" line, "Dear Ms. Rivera:" (colon), body, "Sincerely," then name; "Enclosures:" line if any.
- **uk:** sender address top right or letterhead, date as "3 October 2026", recipient address on the left, "Dear Ms Rivera," (no full stop after titles) closing "Yours sincerely,"; "Dear Sir or Madam," closing "Yours faithfully,"; optional bold subject line after the salutation.
- **de (DIN 5008):** sender line and recipient address field top left, information block or date on the right ("3. Oktober 2026" or "03.10.2026"), reference line ("Ihr Zeichen", "Kundennummer"), bold subject line without the word "Betreff", "Sehr geehrte Frau Müller," or "Sehr geehrte Damen und Herren," then the first sentence starting in lower case, closing "Mit freundlichen Grüßen" with no comma, "Anlagen" listed at the end.
- **fr:** sender block top left, recipient block on the right, "À Paris, le 3 octobre 2026", "Objet :" line, optional "Références :", salutation "Madame," / "Monsieur," / "Madame, Monsieur,", a full closing formula that repeats the salutation ("Je vous prie d'agréer, Madame, Monsieur, l'expression de mes salutations distinguées."), signature, "Pièces jointes :".
- **br:** place and date "São Paulo, 3 de outubro de 2026", recipient block, "Assunto:" line, "Prezado Senhor," / "Prezada Senhora," or "Prezados Senhores," (use "Ilustríssimo Senhor" only for very formal public bodies), closing "Atenciosamente," then name and CPF or CNPJ if relevant.
- **generic:** neutral international block format, date written out with the month as a word, subject line, "Dear …," and "Yours sincerely,".
</context>

<task>
Write a formal letter for this purpose, to $recipient, using the $country_convention convention.

<purpose>
$purpose
</purpose>
Only if facts_and_references was provided: 
<facts_and_references>
$facts_and_references
</facts_and_references>

1. If the purpose is unclear (you cannot tell what the recipient should do), ask one or two questions and stop.
2. Language: for de, fr and br, write the letter in German, French or Brazilian Portuguese unless the user asks otherwise, and give an English line-by-line gist under Translation notes so the sender knows what they are signing. For us, uk and generic, write in English unless the purpose is written in another language, in which case use that language.
3. Structure the body:
   - Opening paragraph: who you are in relation to the recipient (customer, resident, parent, supplier) and the purpose in one or two sentences, with the reference numbers.
   - Middle: the relevant facts in date order, short and verifiable, with amounts and dates exactly as supplied.
   - Request: the exact action, the deadline for it and, if useful, how to reply (address, email, phone placeholder).
   - Close: enclosures and one courteous line; no grovelling, no threats unless the user explicitly wants a firm notice, in which case state the next step calmly.
4. Fill the layout for the chosen convention. Use placeholders in square brackets (`[Your full name]`, `[Customer number]`) for anything not supplied. Never invent account numbers, names, addresses, dates or legal references.
5. Choose the salutation and closing correctly for whether a named person is known.
</task>

<constraints>
- One page: body under about 300 words.
- Formal but plain. Short sentences. No idioms that do not translate.
- If the letter cancels a contract, disputes a charge, responds to an official decision or has a legal deadline, say under Before you send that deadlines, notice periods and the right form of delivery (registered post, signature, online portal) should be checked, without asserting what they are.
- Do not cite laws, articles or regulations unless the user supplied them.
</constraints>

<output_format>
## Letter
The complete letter in a code block or as plain text with line breaks, laid out top to bottom as it should be printed.
## Translation notes
For de, fr and br: an English gist of each paragraph and any etiquette choice explained in one line. Otherwise "Not applicable".
## Before you send
Bullets: placeholders to fill, enclosures to attach, signature, delivery method to consider, and any deadline to check.
</output_format>
