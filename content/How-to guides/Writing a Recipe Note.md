---
publish: true
title: Writing a Recipe Note
created: 2026-07-31T12:52
modified: 2026-10-01T15:00
---

A Recipe Box recipe is a normal Markdown note with some frontmatter properties and two headings - one for ingredients, one for instructions. Everything else in the note is yours; Recipe Box only reads what it needs.

## Minimal Example

```markdown
---
type: recipe
servings: 4
prep: 10
cook: 20
diet: [vegetarian]
allergens: [dairy, gluten]
---

# Spaghetti Aglio e Olio

## Ingredients

- 1 lb spaghetti
- 1/2 cup olive oil
- 6 cloves garlic, thinly sliced
- 1/2 tsp red pepper flakes
- Fresh parsley, chopped #Herb

## Instructions

1. Boil the spaghetti for 9 minutes until al dente.
2. While the pasta cooks, gently warm the olive oil and garlic in a pan for 5 minutes.
3. Toss the drained pasta with the garlic oil, pepper flakes, and parsley.

## Notes

Additional sections below the instructions - including one matching your **Notes heading** setting (default `## Notes`) - are shown in the recipe view. Use this area for notes, variations, extra images, etc.
```

## Frontmatter Properties

All properties are optional unless noted. Property names are configurable in **Settings → Recipe Box** (the table below shows the defaults); Recipe Box also accepts a few common aliases for convenience.

| Property                         | Default key                           | Description                                                                                                                       |
| -------------------------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Type                             | `type`                                | Set to your configured **Recipe type value** (default `recipe`) so Recipe Box recognizes the note as a recipe.                    |
| Image                            | `image`                               | Hero image. Accepts a vault-relative path or a URL. Falls back to a placeholder if missing or unresolved.                         |
| Multiplier                       | `multiplier`                          | Portion scale factor (default `1`). Written automatically when you use the +/- stepper in the recipe view.                        |
| Servings                         | `servings`                            | Number of servings the recipe makes as written.                                                                                   |
| Calories / Protein / Fat / Carbs | `calories`, `protein`, `fat`, `carbs` | Nutrition values. Whether these represent the whole recipe or a single serving is controlled by **Nutrition source** in settings. |
| Prep time / Cook time            | `prepTime`, `cookTime`                | In minutes. `totalTime` is computed from `prepTime + cookTime` if omitted.                                                        |
| Diet                             | `diet`                                | A diet tag or list of tags (e.g. `vegan`, `[vegan, gluten-free]`). Shown as badges in the recipe view.                            |
| Allergens                        | configurable, default `allergens`     | CSV text or a YAML list of allergens (e.g. `[dairy, tree nuts]`). Compared against **My allergens** to show warnings.             |
| Favorite                         | `favorite`                            | `true` to mark the recipe as a favorite.                                                                                          |
| Last made                        | configurable, default `lastMade`      | Auto-stamped `YYYY-MM-DD` date. Derived from the `cookHistory` array whenever cook history is on.                                 |
| Cooked count                     | `cookedCount`                         | Auto-derived from the number of cook history entries whenever cook history is on.                                                 |
| Cook history                     | configurable, default `cookHistory`   | Array of `{id, date, note}` objects written by Recipe Box. Do not edit by hand - use the Cook History modal or tab.               |
| Rating                           | configurable, default `rating`        | A 1-5 rating, shown as stars in the recipe view title.                                                                            |

> [!Note] Source Link
> If your frontmatter includes any of `source`, `url`, `link`, `website`, or `recipe_url`, Recipe Box shows it as a clickable link in the recipe view's mobile Info tab.

## The Ingredients Section

Add a heading matching your **Ingredients heading** setting (default `## Ingredients`), followed by a bullet list. Recipe Box extracts every list item under that heading, until the next heading of the same or higher level.

### How an Ingredient Line Is Parsed

Each line is run through a parsing pipeline that extracts a quantity, unit, and ingredient name:

1. **List markers** (`-`, `*`, `+`, `1.`) are stripped.
2. **Markdown emphasis** is stripped: bold (`**text**`), underline (`__text__`), and paired single-asterisk emphasis (`*text*`, RecipeMD's convention for marking an amount - e.g. `*600g* flour`). A bare or unpaired asterisk is left alone, so `2*3 cups stock` isn't touched. Single underscores are also left alone.
3. **Trailing tags** (`#Tag`, e.g. `#Produce`, `#IgnoreIngredient`) are pulled off and recorded separately.
4. **Trailing notes** in parentheses or after a comma are stripped from the name but kept in the raw line.
5. **Quantity** is parsed from the start. Supported: whole numbers, decimals including a leading decimal point (`.5`), decimals using a comma divider (`1,5`), fractions (`1/2`, `1 1/2`), unicode fractions (`½`, `1½`, `1 ½`), articles (`a pinch of salt` → quantity 1), and ranges (`2-3`, `1/2 to 3/4`). See [[#Ranges and Second Measurements]].
6. **Unit** is normalized through a synonym table (`tbsp`, `tablespoon`, `tbs` → same unit; `g`, `gram`, `grams` → same unit). You can add your own unit words, such as localized units like `EL` or `tasse`, under **Settings → Recipe Box → Recipe parser**. See [[Mapping Ingredient Units]].
7. **Second measurement** (optional): a `/` or `|` followed by another amount and unit, such as `125 g / 4 oz`, is recorded separately.
8. The remainder becomes the normalized **ingredient name**.

Examples:

| Line | Quantity | Unit | Name |
|---|---|---|---|
| `2 cups flour` | 2 | cup | flour |
| `1/2 cup milk` | 0.5 | cup | milk |
| `1 1/2 lbs ground beef` | 1.5 | lb | ground beef |
| `.5 teaspoon salt` | 0.5 | tsp | salt |
| `1,5 kg potatoes` | 1.5 | kg | potatoes |
| `a pinch of salt` | 1 | pinch | salt |
| `2-3 bananas` | 2-3 | - | bananas |
| `1 cup / 240 ml water` | 1 (second: 240 ml) | cup | water |
| `Fresh parsley, chopped #Herb` | - | - | fresh parsley (tag: Herb) |

A comma only divides digits, so text after an amount is unaffected: `2, peeled onions` still parses as quantity 2 with `, peeled onions` as the remainder.

### Ranges and Second Measurements

**Ranges.** Write a range with a hyphen, an en or em dash, or the word `to`:

| Line | Parsed as |
|---|---|
| `2-3 bananas` | 2 to 3, name `bananas` |
| `2 – 3 cups flour` | 2 to 3 `cup`, name `flour` |
| `1/2 to 3/4 cup milk` | 1/2 to 3/4 `cup`, name `milk` |
| `2 1/2-3 cups stock` | 2 1/2 to 3 `cup`, name `stock` |
| `2-3 12 oz cans tomatoes` | 2 to 3, name `12 oz cans tomatoes` |

A dash or `to` only starts a range when a number follows it and the second number is at least as large as the first. So these are **not** ranges:

- `2-inch piece ginger` → quantity 2, name `inch piece ginger`
- `1-2-3 sauce` → quantity 1, name `2-3 sauce`
- `2-2 eggs` → quantity 2 (a range with equal ends collapses to one number)

The recipe view shows the range with an en dash (`2–3`) and scales both ends. Anywhere Recipe Box needs a single number, such as the grocery list, it uses the **upper end** of the range, so you buy enough.

**Second measurements.** Recipes often give an amount in two unit systems. Separate them with `/` or `|`, with or without spaces:

| Line | First | Second | Name |
|---|---|---|---|
| `125 g / 4 oz rice sticks` | 125 `g` | 4 `oz` | rice sticks |
| `1 cup/240 ml water` | 1 `cup` | 240 `ml` | water |
| `8 cups\|1892 ml water` | 8 `cup` | 1892 `ml` | water |
| `1/2 cup / 1 stick butter` | 1/2 `cup` | 1 `stick` | butter |

Rules:

- The first amount must have a recognized unit, and the second must be a number followed by a recognized unit. Otherwise the slash stays in the name: `1 can / tin of beans` keeps the name `/ tin of beans`, and `2 eggs / 100 g` keeps the name `eggs / 100 g`.
- Custom [[Mapping Ingredient Units|unit mappings]] apply to both measurements.
- The second measurement is shown in the recipe view and scales with the multiplier, but it is **display only**. The grocery list and merging use the first measurement.
- Write a second measurement in parentheses (`1 cup (240 ml) milk`) and it's treated as a note instead: shown under the name, not scaled.

### Linked Ingredient Names

If an ingredient's name is a Markdown link, e.g. `- [tomato sauce](sauce.md)`, the link text (`tomato sauce`) becomes the ingredient name and displays as a clickable link in the recipe view. A linked ingredient and a plain one with the same name merge on the grocery list - `[tomato sauce](sauce.md)` and a plain `tomato sauce` share one grocery entry. Wikilinks (`[[tomato sauce]]`) are unwrapped the same way, honoring an alias when one is given (e.g. `[[sauce.md|tomato sauce]]`).

### Excluding a Line from the Grocery List

Add `#IgnoreIngredient` as a trailing tag to keep the ingredient visible in the recipe but exclude it from grocery list generation:

```markdown
- Salt and pepper, to taste #IgnoreIngredient
```

### Tagging Ingredients for Category Grouping

Trailing `#Tag`s double as category hints when **Category source** is set to "recipe tags" or "tag, then dictionary" - see [[Categorizing Grocery Items]].

### Subheadings within Ingredients

You can group ingredients under subheadings (e.g. `### For the sauce`) - Recipe Box preserves these groups when displaying the recipe, though grocery list aggregation flattens them.

## The Instructions Section

Add a heading matching your **Instructions heading** setting (default `## Instructions`), followed by a numbered or bulleted list of steps.

- Steps can be grouped under subheadings - these are shown as section headers in the recipe view.
- Any duration phrase in a step is detected and turned into a clickable timer button - see [[Recipe Timers]].

## Notes Written Without Headings (RecipeMD Style)

Recipe Box also reads notes formatted in the [RecipeMD](https://recipemd.org/) style, which separates title, ingredients, and instructions with thematic breaks (`---`, `***`, or `___`) instead of headings:

```markdown
# Spaghetti Aglio e Olio
---
- *1 lb* spaghetti
- *1/2 cup* olive oil
- *6 cloves* garlic, thinly sliced
---
1. Boil the spaghetti for 9 minutes until al dente.
2. Warm the olive oil and garlic in a pan for 5 minutes.
3. Toss the drained pasta with the garlic oil.
```

This only applies when your configured **Ingredients heading** and **Instructions heading** aren't found in the note - an explicit heading always takes precedence, and a note with neither a heading nor this thematic-break structure behaves as before.

- **Ingredients** are read from the bulleted block between the two thematic breaks. Headings inside this block (e.g. `## For the sauce`) title their groups, same as in the heading-based format.
- **Instructions** are everything after the second thematic break, treated as the method in full - not split further by heading detection.
- The closing thematic break may be omitted if the recipe has no instructions, but only when everything after the opening break reads as an ingredient block (bullets and group headings only). A numbered line after the opening break means the note has instructions and simply contains a horizontal rule, not that instructions are absent.

## The Cook History Section

If **Track cook history** is enabled, Recipe Box manages a `## Cook History` section in the note body. This section is fully generated by the plugin from the `cookHistory` frontmatter array - **do not edit it by hand**, as your changes will be overwritten on the next cook. Use the Cook History modal (desktop) or the Cook History tab (mobile) to add, edit, or delete entries.
