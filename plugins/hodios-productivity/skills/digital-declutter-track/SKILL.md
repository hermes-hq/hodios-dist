---
name: digital-declutter-track
description: Runs a digital declutter in gated steps - subscriptions and accounts, files and downloads, photos, email, phone apps and notifications - and ends with a light routine to keep it tidy.
license: CC0-1.0
arguments:
  - devices
  - hours_per_step
argument-hint: <devices> [hours_per_step]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: tech-help
  source: https://hermes-ide.com/prompts/digital-declutter-track
  catalog: 2026.1004.2
---

# Digital declutter track

## Inputs

- `devices` (required): The devices and main services you use, for example "Android phone, Windows laptop, Gmail, Google Photos, iCloud from an old iPhone, too many streaming services".
- `hours_per_step` (optional; default: 1): Roughly how many hours you want to spend on each step.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Guides a digital declutter one area at a time, pausing after each step so the person does the work on their own devices and reports back. Each step fits the time per step chosen and ends with something visibly lighter. The order goes from what costs money, to what fills storage, to what steals attention.

Devices and services: $devices
Hours per step: $hours_per_step

Throughout: fit every instruction to the devices and services named, and say where menu names may differ by version. Back up before deleting anything that cannot be replaced, and prefer archiving to deleting when unsure. Never close an email account or delete an account that is used to sign in to other services or to recover them without first moving those links. Never ask for passwords or codes. If something looks like a hacked account, an unknown device signed in, or monitoring software the person did not install, pause the declutter and suggest dealing with that first.

## Steps

Work through these steps in order. Do not skip a gate.

1. subscriptions-and-accounts (operate)
2. files-and-downloads (operate)
3. photos (operate)
4. email (operate)
5. apps-and-notifications (operate)
6. maintenance-routine (maintain)

### Step 1: Subscriptions and accounts

Stop paying for what is not used and close accounts that are only a risk.

1. Find subscriptions: suggest checking the last two or three months of bank and card statements, the app store's subscriptions page on each phone, and an email search for words like "receipt", "renewal", "subscription" and "trial".
2. List them with the person in a table: service, cost, billing cycle, last used, and keep, cancel, downgrade or share (family plan). Flag free trials that will start charging.
3. Cancel through the official account page or app store, and note the date the access ends.
4. Old accounts: list sign-ups they no longer use (old shops, forums, apps). For each one to close, download any data they want first, remove saved cards, then delete the account through its settings. Skip accounts used to sign in elsewhere (for example "Sign in with Google") until those links are moved.
5. Note the monthly saving.

Stop and ask the person to report what they cancelled and closed before moving on to files.

**Gate:** stop here and wait for the user's approval before step 2 (files-and-downloads).

### Step 2: Files and downloads

Clear the clutter that hides the files that matter.

1. Make sure a backup exists or make one before deleting (the system's backup tool or a cloud copy).
2. Downloads folder: sort by size, then by date; delete installers and duplicates, and move anything worth keeping into the right folder.
3. Desktop: move everything into a single "To sort" folder so the desktop is clean today, then sort it in short sessions.
4. A simple folder structure, no more than five top folders (for example Home and money, Work, Family, Projects, Archive), with dates at the start of file names where it helps sorting.
5. Find the largest files and folders with the system's storage view and decide on each.
6. Empty the bin only after a quick final check.

Stop and ask the person what they cleared before moving on to photos.

**Gate:** stop here and wait for the user's approval before step 3 (photos).

### Step 3: Photos

Make the photo library smaller and easier to enjoy, without risking memories.

1. Check the photos are backed up (a cloud photo service or a copy on a computer or drive) before deleting anything.
2. Quick wins: screenshots, blurry shots, duplicates and near-duplicates, and photos of receipts or parking spaces. Many photo apps have screenshot and duplicate views; say where to look on the devices named.
3. Videos take the most space: review the largest ones first.
4. Mark favourites as they go so the best photos are easy to find.
5. If photos are split across services (for example an old iCloud and Google Photos), note it and suggest a separate, deeper session to consolidate them.

Stop and ask the person to report back before moving on to email.

**Gate:** stop here and wait for the user's approval before step 4 (email).

### Step 4: Email

Quieten the inbox and keep it quiet.

1. Unsubscribe from newsletters and shops they do not read, using the unsubscribe option the email service shows, starting with the senders who email most.
2. Archive everything older than a chosen date (for example 60 days) in one go after a quick search for anything starred or from key people.
3. Set two or three filters: receipts to a folder, newsletters they keep to a "Read later" folder, and anything else they always ignore.
4. Keep folders few: Action, Waiting, Receipts and Archive is enough for most people.
5. Delete large old attachments if storage is short, using the email service's size search.

Stop and ask the person how the inbox looks now before moving on to phone apps and notifications.

**Gate:** stop here and wait for the user's approval before step 5 (apps-and-notifications).

### Step 5: Phone apps and notifications

Take back attention from the phone.

1. Delete apps not opened in the last three months, using the phone's list of apps or storage view. Check before deleting anything that holds data not stored elsewhere (notes, authenticator codes, offline maps).
2. Home screen: only the tools used daily on the first screen; time-draining apps moved into a folder on a later screen.
3. Notification audit: go through the notification settings app by app and keep only people (messages, calls) and genuinely time-sensitive alerts (bank, travel, deliveries). Turn off badges and sounds for the rest.
4. Set a focus or do-not-disturb schedule for sleep and one focused block of the day.
5. Ask how the phone feels after a day and adjust.

Stop and ask the person to report back before setting up the maintenance routine.

**Gate:** stop here and wait for the user's approval before step 6 (maintenance-routine).

### Step 6: A light maintenance routine

Keep it tidy with small, regular habits instead of another big clear-out.

1. Weekly, 10 minutes: clear the downloads folder and desktop, archive the inbox, delete the week's screenshots.
2. Monthly, 30 minutes: check subscriptions against the bank statement, review new apps, and check backups ran.
3. Every three months: review notification settings and the largest files and videos.
4. Suggest putting these as repeating reminders in their calendar.
5. Wrap up: what they cancelled and saved, the space freed, and what changed day to day.

This is the last step.
