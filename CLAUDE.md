# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Custom CSS theme for [Miniflux](https://miniflux.app/) RSS reader. Single file (`theme.css`), no build step. Apply by pasting into Miniflux Settings > Custom CSS.

## Setup

1. Paste `theme.css` into **Miniflux Settings > Custom CSS**
2. Set **External font hosts** to: `fonts.googleapis.com fonts.gstatic.com`

## Architecture

The theme is one CSS file with this structure:
1. **Google Fonts import** (Literata + Inter)
2. **Design tokens** in `:root` CSS variables (light mode defaults)
3. **Dark mode overrides** via `@media (prefers-color-scheme: dark)`
4. **Component styles** — base, header, pagination, feed list, article view, forms, etc.

All styling uses CSS variables defined in `:root`. To change colors, only edit the token block (lines ~6–47). The rest of the file references `var(--token)`.

## Color System

Colors come from **Tailwind/shadcn stone** (neutrals) and **orange** (accent) palettes:

| Token | Light | Dark |
|-------|-------|------|
| `--bg` | stone-100 `#f5f5f4` | stone-700 `#44403c` |
| `--text` | stone-900 `#1c1917` | stone-200 `#e7e5e4` |
| `--accent` | orange-700 `#c2410c` | orange-600 `#ea580c` |
| `--accent-hover` | orange-600 `#ea580c` | orange-300 `#fdba74` |

Borders use solid stone hex values, not `rgba()`.

## Typography

- **Body/articles:** Literata (Google Fonts), Georgia fallback
- **UI chrome** (nav, buttons, meta): Inter (Google Fonts), system sans-serif fallback

## Key CSS Patterns

- **All overrides use `!important`** — Miniflux's built-in styles are aggressive and require it
- **Action buttons** ("Mark as read", "Star") are `<button>` elements inside `.item-meta-icons`, not `<a>` links — target both `a` and `button` selectors
- **Category tags** use outline chip style (`border: 1px solid var(--accent)`) with transparent background. They must not show `:visited` state
- **Keyboard-highlighted entry** (`.item.current-item`) uses neutral `--accent-bg` elevation + left accent border
- Hidden elements: `(+)` subscribe link, external article links in meta, top pagination

## Miniflux HTML Reference

Templates are Go templates embedded in the miniflux/v2 binary. Key structures:
- Entry list items: `<article class="item">` with `<header class="item-header">` and `<div class="item-meta">`
- Action buttons: `<button>` inside `<ul class="item-meta-icons">` with `data-toggle-status` / `data-toggle-starred` attributes
- Category tags: `<span class="category"><a href="...">`
- Unread counters: `.unread-counter-wrapper` / `.counter`
- Current item (keyboard nav): `.item.current-item`
