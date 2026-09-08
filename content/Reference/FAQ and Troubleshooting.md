---
publish: true
title: FAQ and Troubleshooting
created: 2026-09-04T15:49:51.118Z
modified: 2026-09-08T15:29:39.144Z
---

## My Note Isn't Opening as a Recipe

Check three things:

1. The note's frontmatter has `type:` set to your **Recipe type value** (default `recipe`).
2. The note is inside one of your configured **Recipe folders** (or that setting is empty, meaning the whole vault).
3. **Auto-open recipe view** is enabled. If it's off, use the **Open as recipe** command instead.

## How Do I Organize My Recipes Into Categories?

Recipe Box doesn't have a separate categorization feature - it uses two things Obsidian and the plugin already support:

- **Folders**, for a single hierarchy (e.g. `Recipes/Breakfast`, `Recipes/Dinner`). Recipe Box's folder scope, and the [[Gallery View]]'s folder filter, both include subfolders automatically - no extra setup needed beyond creating the subfolders.
- **Tags** (`#pasta`, `#soup`, anywhere in the note, or a `tags:` frontmatter list), for categories that cut across your folder structure. A recipe can carry multiple tags at once, which a folder can't do - use tags when a recipe belongs to more than one category (e.g. `#dinner` and `#pasta` on the same note). Tags are filterable in the [[Gallery View]] and usable as a scoring field in [[Meal Suggestions]].

Combine both: folders for the one grouping that matters most to how you browse, tags for everything else.

## My Ingredients Aren't Showing Up / Aren't Being Parsed Correctly

- Make sure your ingredient list is a bullet or numbered list directly under a heading matching **Ingredients heading** (default `## Ingredients`).
- If there's no matching heading, Recipe Box falls back to every bullet list in the note - which can pick up unrelated lists. Add the heading to be safe.
- Lines like "Salt and pepper to taste" with no leading quantity are still added but with no quantity/unit.

## An Ingredient Keeps Landing in "Other"

The built-in dictionary doesn't recognize it. Add a [[Categorizing Grocery Items|category override]], or tag it with `#Category` on the ingredient line and switch **Category source** to "Tag" or "Tag, then dictionary".

## Quantities Aren't Combining the Way I Expect

Items combine when their normalized **name and unit** match exactly. "2 cups flour" and "1 cup all-purpose flour" won't merge if the names normalize differently. Try keeping units and naming consistent across recipes for ingredients you buy often.

## I Added/Removed a Recipe from the Meal Plan but the Grocery List Didn't Update

Run **Sync grocery list from meal plan note**. This is also the fix if you edited the meal plan note by hand.

## My Multiplier Isn't Scaling Nutrition/Servings the Way I Expect

Check **Nutrition source** - it tells Recipe Box whether the numbers in your frontmatter are recipe totals or per-serving. If it's set the opposite of how you actually entered your numbers, scaling and the per-serving/total toggle will look wrong.

## Timers Aren't Appearing

- Confirm **Enable timers** is on.
- Recipe Box only detects phrases that look like durations (e.g. "for 10 minutes", "10-15 min", "1 hour"). Rephrasing a step to include a clear duration phrase usually fixes detection.

## I Don't See Meat Temperature / Allergen / GI Badges

- Meat temperature badges require **Show meat temperature warnings** on, and only appear for ingredients Recipe Box recognizes as meat/fish/shellfish (not broths or sauces).
- Allergen warnings require **My allergens** to be set, and the recipe's allergens to overlap with your list.
- High-GI badges require **Diabetic mode** on and the ingredient to match your **GI dictionary**.

## "Suggest a Meal" Isn't Suggesting Anything

- Confirm your recipes have `type` matching **Recipe type value** and live in a configured recipe folder.
- Lower **Suggestion day window** (or set it to `0`) if everything was cooked recently.
- If "Favorites only" is checked, make sure enough recipes have `favorite: true`.

## My Cook History Entries Disappeared After a Write

The `## Cook History` section in the note body is managed by Recipe Box and regenerated from the `cookHistory` frontmatter array on every write. If you edited the note body directly inside that section, your changes were overwritten. Use the Cook History modal (desktop) or Cook History tab (mobile) to add, edit, or delete entries - never edit the note body section by hand.

## lastMade / cookedCount Don't Match My History

If **Track cook history** is on, `lastMade` and `cookedCount` are derived from the `cookHistory` frontmatter array automatically - they are not independently managed. If these values look wrong, check the `cookHistory` array in the note's frontmatter. Editing `lastMade` or `cookedCount` directly while cook history is on will have no lasting effect, as they'll be overwritten on the next cook.

## I Cleared My Grocery List by Accident

**Clear grocery list** clears the grocery list note and Recipe Box's item state immediately, with no in-app undo. If your vault is under version control or has file history (e.g. Obsidian Sync's file recovery), restore the note from there.

## Where Is My Data Actually Stored?

In your notes. Recipe metadata (including cook history) lives in each recipe's frontmatter; the meal plan and grocery list are plain Markdown notes at the paths you configure. Recipe Box's plugin data file additionally tracks meal plan entries, one-off items, and which groups you've collapsed - but the notes are the source of truth for what you see.

## Still Stuck?

Check the [GitHub repository](https://github.com/AdamArcane/recipe-box) for issues and releases, or open a new issue with your settings and an example recipe note (with any sensitive info removed).
