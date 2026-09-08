---
publish: true
title: Settings Reference
created: 2026-07-01T10:59
modified: 2026-07-21T14:30
---

All Recipe Box settings live under **Settings → Recipe Box**, organized into the sections below. Defaults are shown in _italics_.

## Notes & Storage

| Setting | Default | What it does |
|---|---|---|
| Meal plan note path | _`Meal Plan.md`_ | Where Recipe Box reads/writes your meal plan note. Supports Moment.js format tokens for dated notes. See [[Setting Up Meal Plan and Grocery Notes]]. |
| Grocery list note path | _`Grocery List.md`_ | Where Recipe Box reads/writes your grocery list note. Supports Moment.js format tokens. |
| Ingredients heading | _`Ingredients`_ | The heading Recipe Box looks for to find a recipe's ingredient list. |
| Instructions heading | _`Instructions`_ | The heading Recipe Box looks for to find a recipe's cooking steps. |
| Notes heading | _`Notes`_ | The heading Recipe Box looks for to find a recipe's optional notes section. |

## Recipe Library

| Setting              | Default         | What it does                                                                                                                                                                                                                                                                 |
| -------------------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Recipe folders       | _`["Recipes"]`_ | Folder(s) Recipe Box scans for recipes. Requires at least one entry; use `/` to search the entire vault. Deleting the last entry restores the default. Recipe Box warns if `/` is set with no recipe type value, since that combination treats every vault note as a recipe. |
| Recipe type value    | _(empty)_       | Frontmatter `type` value that marks a note as a recipe (e.g. `recipe`). When blank, folder location alone determines detection - no frontmatter required.                                                                                                                    |
| Enable dashboard | _On_ | Shows the single **Recipe Box dashboard** ribbon icon. When off, the separate grocery list / meal plan / gallery ribbon icons are shown instead, and the **Open recipe dashboard** command isn't registered. See [[Dashboard]]. |
| Open gallery when clicking a recipe folder | _Off_ | Clicking a configured recipe folder's name in the file explorer opens the [[Gallery View]] filtered to that folder, instead of expanding/collapsing it. Marked folders get a distinct underline. |
| Also apply to subfolders | _Off_ | Only shown when the setting above is on. Extends the same click behavior to subfolders, filtering the gallery to the specific subfolder clicked. |

## Recipe View

| Setting                 | Default        | What it does                                                                                                                                                                                                                                          |
| ----------------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Strip duplicate title and hero image from body | _On_ | Removes a leading `# Title` from the body if it matches the note title, and removes an inline image if it matches the `image` frontmatter property. One combined toggle. |
| Use first image in note when frontmatter image is empty | _On_ | When the `image` frontmatter property is unset, the recipe view uses the first image found in the note body as the hero image instead. |
| Default recipe image   | _Recipe Box's built-in placeholder image_ | Shown in the recipe view and gallery when a recipe has no frontmatter or body image. Accepts a vault path, wikilink, or URL - same format as the `image` property. Leave blank to fall back to the plain placeholder instead. Never used on public shares. |
| Rating property         | _`rating`_     | Frontmatter property storing a recipe's 1-5 star rating.                                                                                                                                                                                              |
| Cross off while cooking | _On_           | Automatically checks off ingredient list items as you tap them during cooking.                                                                                                                                                                        |
| Show tags in header     | _On_           | Displays the note's frontmatter tags above the badge row in the recipe header.                                                                                                                                                                        |
| Tag prefix              | _On_           | Prefixes each displayed tag with `#`.                                                                                                                                                                                                                 |
| Tag format              | _Last segment_ | Show tags as only the last segment of a nested tag path (e.g. `italian` rather than `cooking/italian`). Toggle off to show the full path.                                                                                                             |
| Auto-open recipe view   | _On_           | Automatically switches a matching note into the [[Recipe View]] when opened.                                                                                                                                                                          |
| Desktop recipe layout   | _Two column_   | Layout style for the desktop recipe view: **Two column** (hero image and ingredients on the left, instructions on the right, with a draggable resizing divider) or **Classic** (single-column, ingredients above instructions). Mobile is unaffected. |
| Reset two-column split  | _(button)_     | Restores the default 50/50 column split for the two-column layout.                                                                                                                                                                                    |

## Recipe Timers

| Setting | Default | What it does |
|---|---|---|
| Enable timers | _On_ | Detects duration phrases in instructions and shows clickable timer buttons. |
| Auto-start timers | _Off_ | Starts the countdown immediately when a timer button is clicked. |
| Default to compact timers | _Off_ | New timers open in compact (time-only) mode. |
| Timer range default | _Max_ | For ranges like "10-15 minutes", whether the timer uses the high (Max) or low (Min) end. |
| Timer increment (minutes) | _1_ | How many minutes the +/- steppers adjust by. |

See [[Recipe Timers]].

## Shopping

| Setting | Default | What it does |
|---|---|---|
| Grouping | _Category_ | Default grouping for the Shopping Assistant: Category, Recipe, Source, or None. |
| Auto-collapse completed sections | _Off_ | Collapses a group automatically when its last unchecked item is checked off. |
| Auto-add ingredients on sync | _Off_ | When syncing the grocery list from the meal plan, automatically add ingredients from newly-discovered recipes. |
| Auto-add ingredients tag | _(empty = all recipes)_ | Restricts auto-add-on-sync to recipes carrying this tag (without the leading `#`). |

See [[Shopping Assistant]] and [[Meal Planning]].

## Categories

| Setting | Default | What it does |
|---|---|---|
| Category source | _Dictionary_ | Where item categories come from: built-in Dictionary, recipe Tags, or Tag-then-dictionary. |
| Auto-sort categories | _On_ | Sorts category groups alphabetically; ignores manual category order when on. |
| Category order | _see below_ | Manual category ordering, used when auto-sort is off. |
| Category overrides | _(none)_ | List of `match` substring → `category` rules, checked before tags/dictionary, longest match first. |

Default category order: Produce, Herb, Meat, Seafood, Dairy, Cheese, Egg, Bread, Pasta, Grain, Canned, Broth, Sauce, Condiment, Oil, Seasoning, Baking, Nuts & Seeds, Snack, Frozen, Beverage, Alcohol, Household, Other.

See [[Categorizing Grocery Items]].

## Cooking & Tracking

| Setting | Default | What it does |
|---|---|---|
| Show mark as cooked button | _On_ | Shows a "Mark as cooked" button in the recipe view's action bar. |
| Ask for date when marking cooked | _Off_ | Prompts for a date instead of using today when marking a recipe cooked. |
| Track last made | _On_ | Stamps the date into `lastMade` when a recipe is marked cooked. Derived automatically from cook history when cook history is enabled. |
| Last made property | _`lastMade`_ | Frontmatter property name used to record the last-made date. |
| Track cooked count | _On_ | Keeps `cookedCount` in sync with the number of cook history entries. |
| Track cook history | _On_ | Enables full cook history - adds a structured `cookHistory` frontmatter array and a managed `## Cook History` section in the note body. Enables the Cook History tab on mobile and the Cook History modal on desktop. |
| Cook history heading | _`Cook History`_ | Heading name for the cook history section in the note body (case-insensitive match). Content under this heading is managed by the plugin and will be overwritten on every write. |
| Cook history property | _`cookHistory`_ | Frontmatter property name for the structured cook history array. |
| Prompt for notes when marking cooked | _On_ | Shows a notes field in the mark-as-cooked dialog; the text is stored in that cook history entry. |
| Track photos | _Off_ | Shows an image picker in the mark-as-cooked dialog; the selected photo is saved as a vault attachment and embedded in the cook history section. |

See [[Cook History]].

## Nutrition

| Setting | Default | What it does |
|---|---|---|
| Nutrition display | _Per-serving_ | Whether the recipe view shows nutrition/servings as per-serving or recipe totals. |
| Nutrition source | _Per-serving_ | Whether the values stored in frontmatter represent a single serving or the recipe total (Recipe Box converts as needed for display). |
| Calories property | _`calories`_ | Frontmatter property for calories. |
| Protein property | _`protein`_ | Frontmatter property for protein (g). |
| Fat property | _`fat`_ | Frontmatter property for fat (g). |
| Carbs property | _`carbs`_ | Frontmatter property for carbs (g). |

## Meal Plan

| Setting | Default | What it does |
|---|---|---|
| Meal type notation | _Tag_ | How meal type (Breakfast, Dinner, etc.) is written in the meal plan note: as a `#tag/slug`, a `[field:: value]` Dataview field, or plain `(text)`. |
| Meal type field name | _`meal`_ | The tag or field name used for meal type (e.g. `meal` produces `#meal/dinner` in tag notation). |

## Meal Recommender

| Setting | Default | What it does |
|---|---|---|
| Modes | _3 built-in modes_ | Named sets of filters and scoring rules. Each mode produces a different ranked list. Click a mode's pencil icon to edit it, the copy icon to duplicate it, or the trash icon to delete it (custom modes only). Set one mode as the default using the radio button. See [[Meal Suggestions]]. |

The result count (5, 7, 10, or 14) is now a selector inside the suggester dialog rather than a global setting. Cooldown logic is expressed as a **filter** inside each mode (e.g. `lastMade` → "not within last 14 days").

## Export

| Setting | Default | What it does |
|---|---|---|
| Export folder | _`Recipe Exports`_ | Default vault-relative folder for Markdown recipe exports. Can be overridden per-export in the export dialog. |
| Default format | _Markdown (plain)_ | Format pre-selected when the export dialog opens. Options: Markdown (plain), Markdown (importable), JSON, JSON-LD. |
| Include cook history by default | _On_ | Pre-checks "Include cook history and other sections" in the export dialog. |
| Include images by default | _On_ | Pre-checks "Include images" in the export dialog. |

See [[Recipe Export]].

## Health & Safety

| Setting | Default | What it does |
|---|---|---|
| Show meat temperature warnings | _On_ | Shows USDA safe minimum internal temperatures next to recognized meat/fish/shellfish ingredients. |
| Allergens property | _`allergens`_ | Frontmatter property holding a recipe's allergens (CSV text or YAML list). |
| My allergens | _(none)_ | Allergens you want to be warned about. |
| High GI warnings | _Off_ | Master toggle for high glycemic-index ingredient badges. |
| GI dictionary | _built-in default_ | Editable regex dictionary (one pattern per line, `#` comments) used to flag high-GI ingredients (GI ≥ 70). |

See [[Health and Safety Warnings]].

## Recipe Import

| Setting | Default | What it does |
|---|---|---|
| Import folder | _(empty = first recipe folder)_ | Vault-relative folder where imported recipes are saved. |
| Import template note | _(empty = built-in default)_ | Vault-relative path to a note used as the template for imported recipes. |

Recipe Box also downloads the recipe's hero image into your vault automatically on import (best-effort, non-blocking) - there's no settings-tab toggle for this yet. See [[Importing Recipes from the Web]].

## Sharing

Sharing a recipe has no dedicated settings section - expiry (7/30/90 days) is chosen per-share in the Share dialog, not set globally. See [[Sharing a Recipe]].

The gallery's folder-click settings above live under **Recipe library**, not a separate settings section. See [[Gallery View]]. The Dashboard's cooking activity chart range (2/4/8/12 weeks) is remembered automatically and has no settings-tab control - it's changed from the chart's own dropdown. See [[Dashboard]].

## Commands

Recipe Box registers these commands (search "Recipe Box" in the Command Palette):

| Command | What it does |
|---|---|
| Open grocery list | Opens the [[Shopping Assistant]] view. |
| Open meal plan | Opens the [[Meal Planning\|Meal Plan view]]. |
| Open recipe gallery | Opens the [[Gallery View]]. |
| Open recipe dashboard | Opens the [[Dashboard]]. Only registered when **Enable dashboard** is on. |
| Import recipe | Opens the recipe import dialog (from URL or pasted text). See [[Importing Recipes from the Web]]. |
| Add grocery item | Opens the add-item dialog. |
| Toggle current recipe in meal plan | Adds or removes the active recipe note from the meal plan (opens the **Add to meal plan** dialog to add; removes all its entries to take it off). |
| Open current file as recipe | Switches the active note into the [[Recipe View]], if it isn't already. |
| Open current file as Markdown | Switches the active note back to plain Markdown. |
| Export current recipe | Opens the recipe export dialog for the active recipe note. See [[Recipe Export]]. |
| Share this recipe | Opens the share dialog for the active recipe note, or manages/revokes its existing link. See [[Sharing a Recipe]]. |
| Suggest a meal | Opens the meal suggestion dialog. See [[Meal Suggestions]]. |

Actions like syncing the grocery list from the meal plan, clearing the meal plan, and exporting the grocery list are buttons inside the [[Shopping Assistant]] and [[Meal Planning|Meal Plan view]] toolbars rather than separate commands.
