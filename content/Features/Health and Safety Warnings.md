---
publish: true
title: Health and Safety Warnings
created: 2026-07-01T09:28
modified: 2026-07-17T09:35
---

Recipe Box can surface a few health and safety cues directly in the recipe view: safe meat cooking temperatures, allergen warnings, and high-glycemic index ingredient flags. None of this is medical advice - it's meant as a helpful nudge, and you should always use your own judgment (and a food thermometer).

![[System/Attachments/Health and Safety Warnings.png]]

## Meat Temperature Warnings

When **Show meat temperature warnings** is enabled, Recipe Box recognizes meat, poultry, fish, and shellfish ingredients by name and shows the USDA-recommended safe minimum internal temperature next to them in the recipe view:

| Category | Safe minimum internal temperature |
|---|---|
| Poultry (chicken, turkey, duck) | 165°F / 74°C |
| Ground meat (ground beef, ground turkey, etc.) | 160°F / 71°C |
| Pork | 145°F / 63°C |
| Beef, lamb, veal | 145°F / 63°C |
| Fish | 145°F / 63°C |
| Shellfish | 145°F / 63°C |

Detection is keyword-based and excludes non-meat preparations like broths, sauces, and stocks that happen to mention a meat name.

## Allergen Warnings

Set **My allergens** to a list of allergens you want to be warned about (e.g. `dairy`, `tree nuts`, `shellfish`). Recipe Box reads each recipe's allergen list from the frontmatter property named by **Allergens property** (default `allergens`, accepts CSV text or a YAML list) and shows a warning banner in the recipe view if any of the recipe's allergens match yours.

This same matching is used by [[Meal Suggestions]] to optionally hide recipes containing your allergens from suggestions.

## High Glycemic-index (GI) Warnings

When **High glycemic index warnings** is enabled, ingredients matching your GI dictionary get a "high GI" badge in the recipe view (GI ≥ 70).

The default dictionary covers:

- Refined grains (white bread, white rice, etc.)
- Starchy preparations (mashed potatoes, etc.)
- Sugars and syrups
- Sugary foods and drinks
- High-GI fruits (watermelon, very ripe banana, etc.)

You can edit the dictionary under **Settings → Recipe Box → Health & safety** - it's a plain-text box, one regex pattern per line, with `#` for comments. Recipe Box validates the dictionary and lets you reset it back to the default if you make a mistake.

This feature is informational only and is not a substitute for medical or dietary advice from a qualified professional.

## Related Settings

**Settings → Recipe Box → Health & safety**: **Show meat temperature warnings**, **Allergens property**, **My allergens**, **Diabetic mode**, **GI dictionary**. See [[Settings Reference]].
