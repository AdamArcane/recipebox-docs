---
publish: true
aliases:
  - Ingredient Filler Word
  - Localized Units
  - Unit Mappings
title: Mapping Ingredient Units
created: 2026-10-01T13:10
modified: 2026-10-01T10:12
---

Recipe Box reads every ingredient line as **quantity, unit, name**. It recognizes a built-in set of English units (`cup`, `tbsp`, `g`, `clove`, and so on). Anything it doesn't recognize stays in the ingredient name, which means `2 Tassen Mehl` is read as "2 of something called _tassen mehl_" instead of "2 cups of flour".

**Unit mappings** let you teach the parser your own unit words, whether they come from another language, an old family cookbook, or your own shorthand. A second setting, **Ingredient filler words**, controls the small connecting words (like `of` or `de`) that sit between the unit and the ingredient name.

## Why It Matters

When a unit is recognized:

- The recipe view shows the unit next to the quantity instead of inside the ingredient name.
- The same ingredient from different recipes **merges** on your grocery list. `2 Tassen Mehl` and `1 cup Mehl` become one `3 cup mehl` line instead of two separate lines.
- Scaled recipes and exports rebuild each line cleanly as quantity, unit, name.

When a unit is not recognized, nothing breaks. The quantity still scales, but the unit word is treated as part of the name, so those items will never merge with anything else.

## Where to Find It

**Settings → Recipe Box → Recipe parser**

The page has two settings:

| Setting | Default | What it does |
|---|---|---|
| Unit mappings | _(none)_ | A list of rows. Each row maps one or more **aliases** to a single **canonical unit**. |
| Ingredient filler words | _`of`_ | A comma-separated list (for example `of, de, di`). The first matching word is removed when it appears right after the quantity or the unit, so `2 cups of flour` becomes `flour`. |

Mappings are added on top of the built-in units. You never need to re-enter `cup` or `tbsp`.

## Adding a Mapping

1. Click **Add unit mapping**.
2. In the first box, type the **aliases**: every spelling you want recognized, separated by commas. Example: `tasse, tassen`
3. In the second box, type the **canonical unit** those aliases should become. Example: `cup`
4. Changes save as soon as you leave a box. Click **Remove** to delete a row.

Rows with an empty aliases box are discarded.

Your recipe notes are **never rewritten**. Mappings are applied every time Recipe Box reads a note, so a new mapping takes effect on existing recipes and on your existing grocery list immediately.

## How Matching Works

These rules decide whether a line matches a mapping:

- **Case doesn't matter.** `EL`, `El`, and `el` are the same alias.
- **Multi-word aliases work.** `cuillère à soupe` is a valid alias.
- **The longest match wins.** With both `c.` and `c. à s.` defined, `2 c. à s. de sel` matches `c. à s.`.
- **A unit has to be followed by a space** (or `,` `;` `:`), or by the end of the line. This is why the alias `t` matches `1 t salt` but does not eat the first letter of `1 tomato`.
- **Trailing periods are ignored.** The alias `stk` matches both `Stk` and `Stk.`, and built-in units work the same way (`tbsp.`, `lb.`, `oz.`). The one exception is the built-in `c`: `c.` is never read as `cup` (see [[#Overriding a built-in]]). Periods _inside_ an alias still count, so `c. à s.` must be written with its periods.
- **Accents are matched regardless of how they are encoded.** Some websites store `è` as a plain `e` plus a separate accent mark. Recipe Box normalizes both your aliases and the recipe text, so they match either way.
- **Your mappings override built-in ones.** If you map an alias that Recipe Box already knows, your version wins.
- **Leaving the canonical unit empty turns the alias into a filler word.** The word is removed from the line and no unit is recorded. This is useful for words like "piece" in other languages, where you want the quantity and name but no unit.

## Choosing a Canonical Unit

The canonical unit is what Recipe Box displays and what it uses to decide whether two items are the same. You have two reasonable options:

**Option A: map to the built-in English unit.** Use one of the canonical units below. Your localized recipes will then merge with any English recipes in your vault. The trade-off is that the recipe view and grocery list display the English abbreviation (`tbsp`) instead of your word (`EL`).

**Option B: map to a unit in your own language.** For example `el, esslöffel -> EL`. Everything displays in your language and all your German recipes merge with each other, but an English recipe using `tbsp` will stay a separate line on the grocery list.

Pick Option A if your vault mixes languages. Pick Option B if nearly all your recipes are in one language.

Whichever you choose, **spell the canonical unit exactly the same way every time.** `cup` and `cups` are different units to Recipe Box and will not merge. The settings page shows a hint under a row whose canonical unit is not built in and not used by any other row, which usually means a typo like `cups`.

### Built-in Canonical Units

`tsp`, `tbsp`, `cup`, `pt`, `qt`, `gal`, `ml`, `l`, `fl oz`, `oz`, `lb`, `g`, `kg`, `mg`, `piece`, `can`, `jar`, `bag`, `box`, `bottle`, `pack`, `bunch`, `head`, `clove`, `slice`, `stick`, `pinch`, `dash`, `sprig`, `stalk`, `loaf`, `dozen`

The words `unit`, `units`, `whole`, and `each` are built-in filler words: they are removed and record no unit.

## Mappings Rename, They Don't Convert

A mapping says "this word means that unit". It does **not** convert between measurement systems. `1 Tasse` mapped to `cup` becomes `1 cup`, not `250 ml`. Likewise, `1 cup milk` and `250 ml milk` remain two separate grocery lines, because they use different units.

## Examples

### German Recipes

| Aliases | Canonical unit |
|---|---|
| `tasse, tassen` | `cup` |
| `el, essl, esslöffel` | `tbsp` |
| `tl, teel, teelöffel` | `tsp` |
| `prise, prisen` | `pinch` |
| `bund` | `bunch` |
| `zehe, zehen` | `clove` |
| `stück, stk` | _(empty)_ |

Filler words: German has no common connector here, so leave it as `of`.

| Recipe line | Without mappings | With mappings |
|---|---|---|
| `2 Tassen Mehl` | 2, name `tassen mehl` | 2 `cup`, name `mehl` |
| `1 EL Zucker` | 1, name `el zucker` | 1 `tbsp`, name `zucker` |
| `1 Prise Salz` | 1, name `prise salz` | 1 `pinch`, name `salz` |
| `3 Stück Eier` | 3, name `stück eier` | 3, name `eier` (no unit) |

### French Recipes

| Aliases | Canonical unit |
|---|---|
| `cuillère à soupe, cuillères à soupe, c. à s.` | `tbsp` |
| `cuillère à café, cuillères à café, c. à c.` | `tsp` |
| `tasse, tasses` | `cup` |
| `pincée, pincées` | `pinch` |
| `gousse, gousses` | `clove` |

Filler words: `of, de`

| Recipe line | Result |
|---|---|
| `1 cuillère à soupe de moutarde` | 1 `tbsp`, name `moutarde` |
| `2 c. à s. de sel` | 2 `tbsp`, name `sel` |
| `1 tasse de farine` | 1 `cup`, name `farine` |
| `1 c. à c. de sel` | 1 `tsp`, name `sel` |

### Your Own Shorthand

Mappings are not only for other languages. If you or an old cookbook use abbreviations Recipe Box doesn't know:

| Aliases | Canonical unit |
|---|---|
| `tbl, tblsp` | `tbsp` |
| `pkg, pkgs` | `pack` |
| `env, envelope, envelopes` | `pack` |
| `qtr` | `qt` |

### Overriding a Built-in

Recipe Box maps `c` to `cup` by default. If that causes problems in your recipes, override it:

| Aliases | Canonical unit |
|---|---|
| `c` | _(empty)_ |

Note that `c.` (with a period) is not treated as `cup` by default, because in many languages it is the start of a longer abbreviation such as `c. à s.`. If your recipes do use `c.` for cup, add a mapping with the alias `c.` and the canonical unit `cup`. If you also have French recipes, map `c. à s.` and `c. à c.` too. Otherwise `c. à s.` is read as `cup` followed by the name `à s. ...`, because the longer alias isn't there to win.

## The Ingredient Filler Words

A filler word is removed in two places: right after the quantity, and right after the unit. With the default `of`:

- `2 cups of flour` → 2 `cup`, name `flour`
- `a pinch of salt` → 1 `pinch`, name `salt`

Things to know:

- **Use a list for mixed-language vaults.** Setting it to `of, de` removes both, so English and French recipes both merge on the plain ingredient name. If you replace `of` with just `de`, `of` is no longer removed.
- **Clearing the box turns filler stripping off.**
- **It matches a whole word followed by a space.** `de` is removed from `de moutarde`, but the elided form in `d'huile` is not, so `2 c. à s. d'huile` gives the name `d'huile`.

## Where Mappings Apply

Unit mappings and the filler word are used everywhere Recipe Box reads an ingredient line:

- [[Recipe View]] ingredient list and scaling
- [[Shopping Assistant]] and the grocery list note, including merging duplicate items
- [[Meal Planning]] when ingredients are auto-added to the grocery list
- [[Recipe Export]] and scaled exports
- Second measurements: in `1 tasse / 250 ml lait`, the `tasse` mapping applies to the first measurement and built-in or custom units apply to the second
- The ingredient editor in the **Add Recipe** dialog (see [[Importing Recipes from the Web]]), so imported lines are split into quantity, unit, and name the same way

## Troubleshooting

**An alias isn't matching.**
Check that the unit is followed by a space (or a period, comma, semicolon, or colon) in the recipe line. `2EL Zucker` with no space does not match. For aliases with internal periods, such as `c. à s.`, check that the spacing in the alias matches the recipe exactly.

**Two items should have merged on the grocery list but didn't.**
Their canonical units are probably spelled differently (`cup` vs `cups`, or `tbsp` vs `EL`), or their names differ after the unit (`of flour` vs `flour`; see the filler word section above).

**I mapped `T` to tbsp and `t` to tsp, and both became the same unit.**
Matching ignores case, so `T` and `t` are the same alias. The last mapping in the list wins. Use distinct spellings instead, such as `tbl` and `tsp`.

**Removing a recipe from the meal plan left some items on the grocery list.**
Recipe Box remembers the ingredients a recipe added using its unit at that time. If you change a mapping while that recipe is on the meal plan, the units no longer line up and those items may need to be removed by hand. Set up your mappings before planning the week.

## Advanced: Stored Format

Mappings are saved in the plugin's `data.json` under `ingredientUnitSynonyms`, as plain text with one mapping per line:

```text
tasse, tassen -> cup
el, essl, esslöffel -> tbsp
stück, stk ->
```

The filler words are saved as `ingredientFillerWord`, as a comma-separated list (`of, de`). An empty value means no filler stripping. You can copy these two values between vaults to share a setup, but edit them through the settings page where possible.

## Related

- [[Writing a Recipe Note]] - how ingredient lines are written
- [[Shopping Assistant]] - where merged grocery items show up
- [[Categorizing Grocery Items]] - the other half of grocery list cleanup
- [[Settings Reference]]
