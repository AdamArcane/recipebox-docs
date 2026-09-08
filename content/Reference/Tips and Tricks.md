---
publish: true
created: 2026-07-01T09:33
modified: 2026-09-04T14:28
---

# Tips and Tricks

A grab-bag of practical tips for getting more out of Recipe Box.

## Recipes

- **Use `#IgnoreIngredient` for staples.** Tag "salt and pepper to taste" or pantry basics you never need to buy with `#IgnoreIngredient` so they stay visible in the recipe but never clutter your grocery list. This only affects ingredients that would be automatically added to the grocery list, not manually selected items.
- **Tag ingredients for category control.** If the built-in dictionary keeps miscategorizing something, either add a `#Category` tag on that ingredient line (with **Category source** set to "Tag" or "Tag, then dictionary") or add a [[Categorizing Grocery Items|category override]] - the override is less work if it's an ingredient you'll see across many recipes.
- **Write quantities Recipe Box can parse.** Plain numbers, decimals, fractions (`1/2`, `1 1/2`, `½`), and "a/an" all parse correctly. Avoid burying the quantity mid-sentence if you want it to scale and aggregate cleanly.
- **Group ingredients and steps with subheadings** (`### For the sauce`) for multi-component recipes - Recipe Box preserves these groupings in the recipe view.
- **Add a source link.** Include `source`, `url`, or `link` in frontmatter for imported recipes - it shows up as a tappable link on mobile.
- **Use folders for one hierarchy, tags for the rest.** A recipe can only live in one folder, but it can carry any number of tags - if you want a recipe to be both "Dinner" and "Pasta," tag it rather than trying to force a folder structure to do both. Both are filterable in the [[Gallery View]].

## Meal Planning & Shopping

- **Sync after manual edits.** If you edit the meal plan note by hand (rename a link, delete a row), run **Sync grocery list from meal plan note** so the grocery list catches up.
- **Use "By recipe" grouping before a big shop** to sanity-check which recipe needs what, especially when scaling recipes up for a dinner party.
- **Use "By source" grouping** to separate what your meal plan needs from what you've manually added.
- **Use Check all / Uncheck all** at the start of a fresh shopping trip instead of clearing everything, if you want to keep your meal plan but start a clean shopping pass.
- **Dated meal plan/grocery notes** (via Moment.js tokens) give you a running history of past weeks - handy for reviewing what you actually cooked.

## Cook History

- **Add notes while the memory is fresh.** The Mark as cooked dialog has a notes field - use it to jot down what you changed, what worked, what didn't. These notes are queryable from Dataview or Bases.
- **Query your cook history with Dataview.** Because cook history is stored as a structured frontmatter array, you can build custom views: all recipes cooked in the last 30 days, recipes you've never made, your most-cooked meals. See the Dataview snippet in [[Meal Suggestions|Meal Suggestions]]
- **Use Cook mode** (sun icon in the recipe header's overflow menu) to keep your screen awake while cooking - tap the icon in the tab header to turn it off when done.

## Scaling Recipes

- The multiplier stepper moves in 0.5 increments and writes back to frontmatter, so a recipe stays scaled the next time you open it. Set it back to `1` to restore original quantities.
- Nutrition and servings figures scale with the multiplier according to your **Nutrition display**/**Nutrition source** settings - double-check these are set correctly if your numbers look off after scaling.

## Health & Safety

- **High glycemic index and meat temperature warnings are independent toggles** - enable one without the other.
- Customize the **GI dictionary** rather than disabling diabetic mode entirely if only a few flagged ingredients don't match your needs - you can comment out lines with `#`.

## Querying Your Recipes

Because everything is Markdown with structured frontmatter, you can build dashboards with Dataview or Obsidian Bases on top of your recipe data:

- A table of all recipes with rating, cuisine, and cook time
- Recipes you haven't cooked in the last 60 days
- Your top 10 most-cooked recipes
- Everything cooked in a given month, with notes

The sample `Recipe Index.base` in this vault shows a starting point for Bases views.

## General

- Recipe Box's plugin data (meal plan entries, one-off items, collapsed groups) is stored in the plugin's own data file, separate from your notes - but the meal plan and grocery _notes_ themselves are the source of truth for what's displayed and can always be edited by hand.
- All recipe data stays in your vault as plain Markdown. You can always access, search, back up, or share your recipes without the plugin installed.
