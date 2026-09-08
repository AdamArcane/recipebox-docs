---
publish: true
created: 2026-07-31T12:52
modified: 2026-07-31T13:25
---

# Writing a Recipe Note

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
5. **Quantity** is parsed from the start. Supported: whole numbers, decimals including a leading decimal point (`.5`), decimals using a comma divider (`1,5`), fractions (`1/2`, `1 1/2`), unicode fractions (`½`), and articles (`a pinch of salt` → quantity 1).
6. **Unit** is normalized through a synonym table (`tbsp`, `tablespoon`, `tbs` → same unit; `g`, `gram`, `grams` → same unit).
7. The remainder becomes the normalized **ingredient name**.

Examples:

| Line | Quantity | Unit | Name |
|---|---|---|---|
| `2 cups flour` | 2 | cup | flour |
| `1/2 cup milk` | 0.5 | cup | milk |
| `1 1/2 lbs ground beef` | 1.5 | lb | ground beef |
| `.5 teaspoon salt` | 0.5 | tsp | salt |
| `1,5 kg potatoes` | 1.5 | kg | potatoes |
| `a pinch of salt` | 1 | - | pinch of salt |
| `Fresh parsley, chopped #Herb` | - | - | fresh parsley (tag: Herb) |

A comma only divides digits, so text after an amount is unaffected: `2, peeled onions` still parses as quantity 2 with `, peeled onions` as the remainder.

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
