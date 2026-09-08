---
publish: true
title: Categorizing Grocery Items
created: 2026-07-01T13:29:44.101Z
modified: 2026-09-08T15:29:39.138Z
---

When grouping by category, Recipe Box needs to decide which category each ingredient belongs to. This is controlled by **Category source**, **Category overrides**, and **Category order** under **Settings → Recipe Box → Categories**.

## Category Sources

**Category source** has three options:

- **Dictionary** (default) - categorize using Recipe Box's built-in keyword dictionary.
- **Recipe tags** - use the trailing `#Tag` on the ingredient line in the recipe (e.g. `- 2 cloves garlic #Produce`). If an ingredient has no tag, it falls back to "Other".
- **Tag, then dictionary** - prefer the recipe's `#Tag` if present, otherwise fall back to the dictionary.

## The Built-in Dictionary

The dictionary matches ingredient names against keyword lists for these categories (also the default category order):

Produce, Herb, Bread, Meat, Seafood, Dairy, Cheese, Egg, Pasta, Grain, Canned, Broth, Sauce, Condiment, Oil, Seasoning, Baking, Snack, Frozen, Beverage, Drinks, Alcohol, Household, Other.

Matching is substring-based and longest-keyword-first, so "ground beef" matches **Meat** and "roma tomatoes" matches **Produce**. Anything unmatched falls into **Other**.

## Category Overrides

**Category overrides** let you force specific ingredients (or substrings) into a category regardless of the dictionary or tags - useful for ingredients the dictionary gets wrong, or personal categories.

Each override is a `match` string (lower-cased, matched as a substring against the ingredient name) and a `category`. Overrides are checked **first**, with longer `match` strings checked before shorter ones. The settings UI offers autocomplete from categories already in use.

Example: if "miso paste" keeps landing in "Other" and you'd rather it sit with your sauces, add an override with match `miso` → category `Sauce`.

## Category Order

When **Auto-sort categories** is off, the grocery list's category groups follow **Category order** (a manually-ordered list). Categories not in the list are appended alphabetically at the end. When **Auto-sort categories** is on, all categories are sorted alphabetically and the manual order is ignored.

## Putting It Together

A typical setup:

1. Leave **Category source** as **Dictionary** unless you tag ingredients in your recipes.
2. Add **Category overrides** for the handful of ingredients the dictionary miscategorizes for your cooking style.
3. Leave **Auto-sort categories** on for simplicity, or turn it off and customize **Category order** to match how your store is laid out.

## Related

- [[Shopping Assistant]] - where category grouping is used
- [[Writing a Recipe Note]] - using `#Tag`s on ingredient lines
- [[Settings Reference]]
