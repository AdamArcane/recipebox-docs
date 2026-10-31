---
publish: true
aliases:
  - bulk import
  - Mealie import
title: Importing Recipes from Files
created: 2026-10-01T17:30
modified: 2026-10-01T17:30
---

Moving from another recipe app? Recipe Box can import a whole collection at once from exported files, turning each recipe into a note in your vault. For a single recipe from a web page or pasted text, see [[Importing Recipes from the Web]].

## Supported Formats

- **Mealie** - recipe exports in `.zip` form (recipes and their images) or as single recipe `.json` files.
- **schema.org Recipe JSON** - any app that exports recipes as schema.org JSON-LD. A file can hold one recipe, a list of recipes, or a `@graph` of several.

## Exporting from Mealie

1. In Mealie, export the recipes you want to move. Pick the recipe export, not a full backup.
2. Save the resulting `.zip` file.

Mealie's **full backup** (the zip that contains `database.json`) can't be imported. It is an internal database dump tied to a specific Mealie version. Recipe Box tells you so if you pick one.

## Importing

1. Run **Import recipes from file** from the Command Palette.
2. Choose one or more `.json` or `.zip` files.
3. Check the pre-flight message, for example "142 recipes found, 3 not recognized". Nothing is written yet.
4. Pick a **destination folder**.
5. Choose what happens **if a note already exists**:
   - **Skip it** (default) leaves the existing note alone.
   - **Keep both** saves the new recipe with a number added, such as `Chili (2)`.
6. Click **Import**. Progress is shown as it runs, and **Stop** ends the import after the current recipe. Notes already created are kept.

When it finishes, a summary lists how many recipes were imported, skipped, or failed, with the file name and reason for anything that wasn't a clean success.

Existing notes are never overwritten, and two recipes with the same name in one import are handled by the same Skip / Keep both choice.

## What Gets Imported

- Title, description, servings, prep, cook, and total time
- Ingredients and instructions, including section headings
- Notes and nutrition (calories, protein, fat, carbs)
- The source URL, when the export includes one
- Images bundled in a Mealie zip. These are always saved to your vault, whatever your **Download images on import** setting says. That setting only controls images that have to be downloaded from a web address.

If an image can't be saved, the recipe still imports without it, and the summary notes it.

## What Doesn't Get Imported

- Tags and categories
- Ratings and cook history
- Meal plans and shopping lists
- Mealie full backups
- Other proprietary formats

## Troubleshooting

- **"Not a recognized recipe format"** - the file isn't Mealie or schema.org Recipe JSON.
- **Very large zips** - Recipe Box reads the whole zip into memory. Above roughly 100 MB you get a warning, and mobile devices may be slow. Splitting the export into smaller zips helps.
