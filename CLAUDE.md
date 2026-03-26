# Miniflux Theme

Custom CSS theme for [Miniflux](https://miniflux.app/) RSS reader, inspired by n+1 magazine's editorial aesthetic.

## Project Structure

- `theme.css` — The entire theme. Paste into Miniflux Settings > Custom CSS.
- `screenshots/` — Visual references.

## Design Decisions

### Typography
- **Body/article text:** Literata (Google Fonts) with Georgia fallback — optimized for long-form reading
- **UI chrome** (nav, meta, buttons, pagination): Inter (Google Fonts) with system sans-serif fallback

### Color Palette
- **Background:** `#f0ebe1` (warm cream)
- **Text:** `#1a1a1a` (near-black)
- **Accent/links:** `#c1440e` (burnt orange)
- **Hover accent:** `#2a7ae2` (blue)
- **Borders:** `rgba(0,0,0,0.08–0.15)` (subtle black alpha)

### Key Styling Choices
- All `!important` overrides — necessary because Miniflux's built-in styles are aggressive
- UI meta text uses reduced opacity (0.55–0.6) for visual hierarchy without separate color tokens
- Category badges: uppercase, small, letter-spaced, in accent color
- Green "unread" highlight on category/feed rows is removed (transparent)
- The `(+)` subscribe button in the header nav is hidden
- External article links in meta are hidden for cleaner layout
- Top pagination is hidden; bottom pagination is kept but subtle

## Setup

1. Paste contents of `theme.css` into **Miniflux Settings > Custom CSS**
2. Set **External font hosts** to: `fonts.googleapis.com fonts.gstatic.com`
3. Click **Update**

## Miniflux HTML Reference

Miniflux templates are Go templates embedded in the binary. Source:
- Layout/header: `internal/template/templates/common/layout.html` in [miniflux/v2](https://github.com/miniflux/v2)
- The `(+)` next to Feeds is a separate `<a href="/subscribe">` element
- Unread counters use `.unread-counter-wrapper` / `.counter` classes
- Feed error counters use `.error-feeds-counter-wrapper` / `.error-feeds-counter`

## Working with This Theme

- This is a single CSS file — no build step needed
- Test changes by pasting updated CSS into Miniflux settings
- Miniflux uses its own base styles, so most overrides need `!important`
- When targeting Miniflux elements, inspect the live page or check the Go templates in the miniflux/v2 repo
