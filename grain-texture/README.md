---
name: Grain Texture
status: production
added: 2026-05-23
last-touched: 2026-05-24
used-in:
  - army-pink (production, every page via body::before in public/styles.css)
tags: [texture, background, global, css-only, no-js]
---

**▶ Live demo**: https://weiyan-design.github.io/design-patterns/grain-texture/example.html

## What it does
A film-grain / letterpress noise overlay that sits above page content via
`body::before`. Adds tactile, filmic warmth to the entire site without
literal animation. Pure CSS — no JS, no image assets to host.

## When to use it
- ✓ Sites with tactile, editorial, or filmic visual identity
- ✓ Wellness, lifestyle, magazine, gallery, or premium brands
- ✓ When you want texture without literal motion (calmer than animated grain)
- ✗ Clean tech / SaaS / modern minimalist aesthetics — fights the look
- ✗ Sites dominated by data viz or photography where grain interferes with read
- ✗ Print (auto-disabled via `@media print`)

## What it depends on
- Browser support for inline SVG data-URIs in CSS `background-image` (all evergreen browsers)
- `<body>` with `position: relative` (or static — most sites have this)
- Awareness of your existing z-index ranges so the grain layer sits in the right tier

## How to integrate (3 steps)
1. Copy the `body::before` rule from `example.html` into your main stylesheet.
2. Set `z-index` based on your stacking context. Default `50` sits *above*
   page content but *below* modal/nav UI (which typically uses 1000+).
3. Tune `opacity` (default `0.3` for "letterpress") and `mix-blend-mode`
   (default `multiply`; try `soft-light` for less aggressive feel on
   media-heavy sites).

## Gotchas
- **`multiply` at 0.3 noticeably darkens photos and videos.** On media-heavy
  pages, drop opacity to 0.15–0.2 or switch to `soft-light`.
- **Always hide in print** — `@media print { body::before { display: none } }`.
- **`pointer-events: none` is required** so clicks pass through to interactive content.
- **High-DPI screens (3x retina)** may show subtle banding in SVG turbulence.
  If visible, swap the inline SVG for a pre-baked PNG noise tile.
- **Don't stack two grain layers** — composite multiply doubles up and goes
  too dark. Pick one (global via body::before, OR a section-specific layer).

## Locked defaults (production-approved 2026-05-24, army-pink)
- Tile size: `240×240`
- Noise: `feTurbulence` with `baseFrequency="0.85"`, `numOctaves="2"`,
  `stitchTiles="stitch"`
- Color matrix: dark gray (RGB ~0.42, 0.40, 0.40)
- Opacity: `0.3`
- Mix-blend-mode: `multiply`
- z-index: `50`
- `position: fixed; inset: 0; pointer-events: none`

## Where it came from
Inspired by Daylight Computer's textured backdrops. First applied site-wide
to Army Pink (2026-05-23) for the wellness-portal aesthetic.

## Open questions / things to reconsider
- A `prefers-contrast: more` media query could disable the grain for users
  who need maximum contrast (not yet implemented).
- For sites that *really* want animated grain, this could be extended to swap
  background-position on a slow interval — though that loses the calm, static feel.
