---
publish: true
title: Customizing Appearance
created: 2026-07-01T09:30
modified: 2026-07-01T12:50
---

Recipe Box integrates with the [Style Settings](https://community.obsidian.md/plugins/obsidian-style-settings) plugin, giving you a UI for tweaking the recipe view and Shopping Assistant's layout without writing CSS.

## Default Appearance

Recipe Box has no built-in theme of its own. Every panel is styled using Obsidian's own CSS variables (spacing, font sizes, colors, border radii, etc.) rather than hardcoded values. In practice this means Recipe Box automatically looks like a native part of Obsidian, matching whatever theme and appearance settings you already have configured.

### How Your Theme Affects Recipe Box

Because Recipe Box pulls its colors, fonts, and spacing from Obsidian's shared CSS variables, any theme you install will reskin Recipe Box automatically:

- **Colors** - backgrounds, borders, muted/faint text, and accent colors all follow your theme's palette.
- **Typography** - font family, sizes, and weights follow your theme's font settings.
- **Spacing and corners** - padding, gaps, and border radii follow your theme's spacing scale.
- **Light/dark mode** - switching Obsidian's color scheme switches Recipe Box's appearance too.

### Relevant Core Obsidian Appearance Settings

| Setting | Effect on Recipe Box |
|---|---|
| Theme | Changes overall colors, spacing, and corner radii throughout Recipe Box's views. |
| Base color scheme (light/dark) | Switches Recipe Box's backgrounds, text, and borders. |
| Accent color | Changes the color of accent elements - quantities, ingredient highlights, and action buttons. |
| Font / Interface font | Changes the typeface used throughout Recipe Box's panels and modals. |
| Font size | Scales text size across Recipe Box's views. |

## Setup

1. Install and enable the **Style Settings** community plugin.
2. Open **Settings → Style Settings**.
3. Find the **Recipe Box** section and expand it.

Changes apply live and are saved by Style Settings - no need to touch `styles.css` yourself.

## Available Options

### Recipe View

| Option | Type | Default | What it does |
|---|---|---|---|
| Max width | Slider, 500-1400px | 900px | Maximum width of the recipe view panel. |
| Hero image aspect ratio | Dropdown | Standard (4:3) | Shape of the hero image: Square (1:1), Standard (4:3), Widescreen (16:9), or Cinematic (2:1). |
| Hide hero image | Toggle | Off | Hides the recipe hero image entirely. |
| Compact ingredients | Toggle | Off | Reduces vertical spacing between ingredient rows. |

### Shopping Assistant

| Option | Type | Default | What it does |
|---|---|---|---|
| Compact grocery list | Toggle | Off | Tighter row height for grocery list items. |
| Compact meal plan panel | Toggle | Off | Tighter row spacing in the meal plan carousel. |

## Without Style Settings

If you don't have Style Settings installed, Recipe Box works exactly the same with its default appearance - Style Settings is purely optional. You can also write your own CSS snippet targeting Recipe Box's classes via **Settings → Appearance → CSS snippets**.

## Related

- [[Recipe View]]
- [[Shopping Assistant]]
- [[Settings Reference]]
