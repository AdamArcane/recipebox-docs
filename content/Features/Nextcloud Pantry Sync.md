---
publish: true
title: Nextcloud Pantry Sync
created: 2026-11-16T12:00
modified: 2026-11-16T12:00
---

Pantry sync keeps your grocery list in step with a checklist in the [Pantry](https://github.com/chenasraf/nextcloud-pantry) app for Nextcloud. Check items off on your phone in the store and they are checked in Obsidian. Add or edit items in either place and the other follows.

It is an optional integration, **off by default**. While it is off, Recipe Box makes no network calls and shows none of its commands. Pantry sync is available from version 0.4.0.

## What You Need

- A Nextcloud server with the Pantry app installed.
- A Nextcloud **app password**. Create one in Nextcloud under **Personal settings → Security**. Use an app password rather than your login password, so you can revoke it on its own.

## Setting It Up

1. Open **Settings → Recipe Box → Integrations → Nextcloud Pantry**.
2. Turn on **Enable Pantry sync**.
3. Fill in **Server address**, **Username** and **App password**. The password is kept in Obsidian's secret storage, not in your notes.
4. Press **Test connection**. A notice tells you how many houses it found.
5. Choose your **House**, then your **Checklist**. To start fresh, press **Create new list** and Recipe Box creates a checklist called "Groceries" for you.
6. Run **Sync grocery list with Pantry** from the Command Palette.

If a dropdown is empty, press the refresh icon next to it. This is common if you chose it before typing your credentials.

## What Syncs

| In Obsidian | In Pantry |
|---|---|
| Checked or unchecked | Done or not done |
| The quantity and unit at the start of a line | The **Quantity** field |
| The rest of the line | The item **Name** |
| The recipes a line came from | The item **Description** |
| A heading that matches a Pantry category | The item's category |

For example, "1 1/2 lb boneless chicken breasts" becomes the quantity `1 1/2 lb` and the name `boneless chicken breasts`.

## How Changes Flow

- **Checking items.** Check an item on either side and it is checked on both after the next sync. If you check it in both places, it ends checked.
- **Editing.** Change a quantity or name in either place and the other side is updated. If you change the same item in both places before a sync, **Pantry wins**.
- **Adding.** A new line in your grocery list is created in Pantry. A new item in Pantry is added to your list, under the heading that matches its Pantry category. If there is no matching heading, one is created. Items with no category go under **Other**.
- **Deleting.** Delete a line and the Pantry item moves to the Pantry trash, where you can restore it. Delete an item in Pantry and its line is removed from your note.
- **Renaming.** Rename a line in Obsidian and the Pantry item is renamed rather than replaced, as long as it is the only line that changed under its heading. If several lines change at once, Recipe Box cannot tell a rename from a delete plus an add, so the old item is trashed and a new one is created.

Recipe names are written into the Pantry description one way only. Recipe Box never overwrites a description you already wrote, and it never reads descriptions back into your note.

Pantry categories are only set when an item is first created. Moving an item to another category in either place does not sync.

## Your Note Stays Plain Markdown

Recipe Box adds nothing hidden to your grocery list. Lines are matched to Pantry items by name and unit, and the links are kept in Recipe Box's plugin data. If that data is lost, the next sync matches lines to Pantry items by name again and does not create duplicates.

## Running a Sync

- **Manually.** Run the **Sync grocery list with Pantry** command, or click **Pantry: synced …** in the status bar.
- **Automatically.** Set **Auto sync every (minutes)** to a number above 0. Recipe Box then syncs on that interval, and a few seconds after you edit the grocery note. Auto sync pauses while you are offline. **0** means manual only.

Turn on auto sync on **one device only**. If two devices push the same new line at once, Pantry can end up with a duplicate.

The status bar shows when the last sync finished, or **Pantry: error** if it failed.

## Good to Know

- Only the first 500 items in a Pantry list are read. Longer lists show a notice.
- If your grocery note is empty but you have synced items, Recipe Box refuses to sync instead of trashing everything in Pantry.
- If Pantry rejects your sign in, auto sync stops until a manual sync works again. Check your app password.
- Pantry's own **Shopping Mode** is not specifically supported. Items you check there reach Obsidian only if Pantry marks them done on the item itself.

## Related

- [[Shopping Assistant]] - the grocery list view that uses the same note
- [[Setting Up Meal Plan and Grocery Notes]] - configuring the grocery note path
- [[Settings Reference#Integrations]] - every Pantry setting
