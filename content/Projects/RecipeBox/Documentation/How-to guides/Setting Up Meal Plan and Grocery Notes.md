---
publish: true
created: 2026-07-01T09:31
modified: 2026-07-01T12:50
---

# Setting Up Meal Plan and Grocery Notes

Recipe Box stores your meal plan and grocery list as ordinary notes. **Settings → Recipe Box → Notes & storage** controls where those notes live.

## Default Setup

By default:

- **Meal plan note path**: `Meal Plan.md`
- **Grocery list note path**: `Grocery List.md`

Both are created at the vault root the first time Recipe Box needs them, with starter content (`# Meal Plan` / `# Grocery List`). If the path includes folders that don't exist yet, Recipe Box creates them.

## Moving the Notes

Change the path (e.g. `Planning/Meal Plan.md`). Recipe Box will read from and write to the new location - it doesn't move your old note automatically, so move or delete it yourself if needed.

## Dated Notes with Moment.js Tokens

Both note paths support [Moment.js format tokens](https://momentjs.com/docs/#/displaying/format/). This lets you generate a fresh note per week, month, etc.

Examples:

| Path setting | Resulting file (example) |
|---|---|
| `Meal Plan.md` | `Meal Plan.md` |
| `Meal Plans/[Week of] YYYY-MM-DD.md` | `Meal Plans/Week of 2026-06-08.md` |
| `Meal Plans/YYYY-[W]ww.md` | `Meal Plans/2026-W24.md` |
| `Grocery Lists/YYYY/MM/[Grocery] YYYY-MM-DD.md` | `Grocery Lists/2026/06/Grocery 2026-06-10.md` |

The token is evaluated when Recipe Box resolves the path, so a weekly token rolls over to a new note automatically when the week changes. Previous weeks' notes stay in your vault as a history of past plans and lists.

> Tip: if you use dated notes, keep your meal plan and grocery list on the **same** cadence so a sync always reads and writes a matching pair.

## Ingredients and Instructions Headings

These settings apply to _recipe_ notes, not the meal plan/grocery notes - see [[Writing a Recipe Note]] for what they do.

## Related

- [[Meal Planning]] - the meal plan note format and workflow
- [[Shopping Assistant]] - the grocery list note format and workflow
- [[Settings Reference]]
