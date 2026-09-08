---
publish: true
title: Getting Started
created: 2026-07-01T09:25
modified: 2026-09-08T08:32
---

## Installation

1. Open Obsidian Settings.
2. Go to **Community Plugins** and make sure restricted mode is off.
3. Click **Browse** and search for "Recipe Box".
4. Click **Install**, then **Enable**.

You can also install a specific release manually from the [GitHub releases page](https://github.com/AdamArcane/obsidian-recipebox/releases/latest) by extracting `main.js`, `manifest.json`, and `styles.css` into `<your vault>/.obsidian/plugins/recipe-box/`.

## Zero-Config Quick Start

On first enable, Recipe Box creates a `Recipes` folder in your vault. Drop any note into that folder and open it - Recipe Box will detect it as a recipe and switch into the recipe view. No frontmatter required.

That's it. Everything below is for customizing how Recipe Box finds your recipes if you want them somewhere else, or if you already have a library organized differently.

## Customizing Recipe Detection

Recipe Box detects recipes using two independent filters, applied with AND logic:

**Folder scope** - Recipe Box only looks at notes inside the configured recipe folders and their sub-folders. The default is `["Recipes"]`. You can add more folders, remove the default, or set a single folder of `/` to search your entire vault. Configure this under **Settings → Recipe Box → Recipe library → Recipe folders**.

> [!Tip] Organizing recipes into categories
> Subfolders are included automatically, so nesting `Recipes/Breakfast`, `Recipes/Dinner`, etc. just works, and both folder scope and the [[Gallery View]]'s folder filter follow them. For categories that cut across a single folder hierarchy (e.g. a recipe that's both "Dinner" and "Pasta"), use tags instead - see [[Tips and Tricks]] and the [[FAQ and Troubleshooting|FAQ]].

**Frontmatter type** (optional) - If you set a **Recipe type value** (e.g. `recipe`), Recipe Box also checks the note's `type` frontmatter property and only treats it as a recipe if it matches. By default this is blank, meaning folder location alone is enough. This is useful when a folder contains a mix of recipe notes and other notes you want to exclude.

The two filters combine: a note must be in a recipe folder AND match the type value (if one is set). Some examples:

- **Folder only (default)**: `recipeFolders: ["Recipes"]`, no type value. All notes in `Recipes/` are recipes, no frontmatter needed.
- **Type only**: `recipeFolders: ["/"]`, `recipeType: "recipe"`. Any note in your vault with `type: recipe` is a recipe.
- **Both**: `recipeFolders: ["Recipes"]`, `recipeType: "recipe"`. Notes must be in `Recipes/` and have `type: recipe`.

> [!Important]
> Setting the folder to `/` with no type value treats every Markdown note in your vault as a recipe. Recipe Box will warn you if this combination is active.
>
> This configuration can cause bad performance depending on the size of your vault and if you have a lot of other non-recipe notes

## Setting Up Notes & Storage

Under **Notes & storage**, set:

- **Meal plan note path** - where Recipe Box writes your weekly meal plan (default `Meal Plan.md`)
- **Grocery list note path** - where Recipe Box writes your grocery list (default `Grocery List.md`)

## Confirming Your Recipe Headings

Recipe Box looks for an **Ingredients heading** and an **Instructions heading** (defaults: `Ingredients` and `Instructions`) in each recipe note. If your recipes use different heading text, update these under **Notes & storage** to match. Don't include any leading `#`.

## Your First Recipe

1. Drop a note into your `Recipes` folder (or whichever folder you configured).
2. Add an `## Ingredients` heading followed by a bullet list of ingredients (e.g. `- 2 cups flour`).
3. Add an `## Instructions` heading followed by a numbered list of steps.
4. Open the note - Recipe Box switches it into the [[Recipe View]] automatically.

## Your First Meal Plan and Grocery List

1. From the recipe view, click **Add to meal plan** (or run the **Add/remove this recipe from meal plan** command).
2. Choose a day and meal type.
3. Open the **Shopping Assistant** (from the [[Dashboard]], or run the **Shopping assistant** command) to see your grocery list, automatically built and grouped from your meal plan.

## Next Steps

- [[Writing a Recipe Note]] - the full frontmatter schema and formatting conventions
- [[Recipe View]] - everything the recipe view shows and does
- [[Meal Planning]] and [[Shopping Assistant]] - the meal plan and grocery workflow
- [[Settings Reference]] - every setting, explained
