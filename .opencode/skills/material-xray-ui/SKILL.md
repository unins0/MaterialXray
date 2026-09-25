---
name: material-xray-ui
description: Use whenever a task creates, changes, or reviews Material Xray's Compose UI, including layout, components, Material 3 theming, palette presets, OLED mode, or visual polish. Enforce the project's clean, dynamic-color-first constraints. Do not use for non-UI VPN, service, data, or parsing work.
---

# Material Xray UI

## Goal

Create a clean native Android interface that is fast to scan and easy to maintain. Use the existing Jetpack Compose and Material 3 stack.

## Non-negotiable rules

- Use only the existing Compose and Material 3 stack; do not add dependencies, UI kits, icon packs, or theme libraries.
- When generic Android UI guidance conflicts with this file, follow these project-specific rules.
- Dynamic color is the default and primary theme on Android 12+.
- Keep the existing simple light and dark schemes only as compatibility fallbacks for Android 11 and older; they are not user-selectable presets.
- Optional user-selectable presets must remain simple static Material 3 color palettes, not a branded palette, parallel token system, component library, or wrapper framework.
- Do not use Material 3 Expressive, `MaterialExpressiveTheme`, expressive shapes, decorative haptics, oversized typography, or expressive motion.
- Do not use blur, glassmorphism, translucent panels, glows, decorative gradients, or background effects.
- Prefer flat surfaces, dividers, lists, and clear spacing over nested cards and elevation.
- Never outline cards with borders or strokes: a card separates itself from the page by its container color alone.
- Preserve existing behavior, state handling, accessibility, and navigation while changing visuals.

## Theme

Keep the implementation in `app/src/main/kotlin/com/material/xray/ui/theme/Theme.kt`. Follow its existing dynamic-color and compatibility-fallback structure.

- Use `MaterialTheme.colorScheme` roles in screens. Do not hard-code colors for ordinary UI.
- Raw colors are acceptable only in fallback themes, static palette presets, syntax highlighting, and overlays that cannot use theme roles.
- Do not override dynamic colors merely to add branding.
- Do not add theme controls unless the task requests them.
- Palette presets are alternatives to dynamic color, not appearance modes. Keep Dynamic as the default and store presets as plain `lightColorScheme` and `darkColorScheme` constants.
- Each selectable palette must provide readable light and dark variants. Do not build a registry, strategy, or plugin layer for a small preset list; a simple `when` is enough.
- Expose OLED as a separate checkbox, not a palette preset. When checked in dark mode, set the background and base surface to black while preserving elevated surface containers, outlines, content colors, contrast, and active dynamic or preset accents. Do not affect light mode.

## Layout and components

- Make connection state and the primary action easy to find.
- Use spacing consistently; prefer a small set of local sizes such as 4, 8, 12, 16, and 24 dp.
- Use `MaterialTheme.shapes`; avoid one-off corner radii.
- Use cards only for grouped, independently meaningful content. Never nest cards.
- Use dividers and list rows for dense settings and server lists.
- Use existing icons and standard Material components.
- Do not create a wrapper for a single call site. Extract a composable only when the same UI and behavior recur across screens.
- Keep screen files focused. For a large screen, redesign one coherent section at a time instead of regenerating the whole file.

## Motion and state

- Use short, standard Material motion only when it explains state changes.
- Do not animate decoration for visual spectacle.
- Always design loading, empty, error, disconnected, connecting, connected, and permission states when relevant.
- Keep touch targets, content descriptions, semantics, and contrast accessible.

## Workflow

1. Read `Theme.kt`, the target screen, and nearby reusable components.
2. Identify the screen's primary task and visual hierarchy.
3. Make the smallest change that improves clarity and consistency.
4. Reuse Material components and semantic theme roles.
5. Check dynamic color, fallback colors, every implemented palette preset, OLED dark mode, long text, and large font scale.
6. Add lightweight previews when useful, but do not introduce a screenshot framework unless requested.
