---
name: Coverflow Doors with Live Tuner
status: experiment
added: 2026-05-24
last-touched: 2026-05-24
used-in:
  - army-pink (production, /wellness-portal hero — tuner removed, defaults baked in)
tags: [layout, hero, carousel, svg, canvas, animation, scroll-driven, 3d, tuner]
---

## What it does
A scroll-driven, perspective-tilted carousel of three "doors" — arch-shaped
image cards with animated wavy bottom edges. The center door is dominant
(sized to fill ~92% of stage height); side doors peek at viewport edges with
a subtle 3D tilt. Vertical scroll rotates the wheel through all three doors.

A cream-on-cream drifting-light canvas backdrop adds atmospheric depth.
The active door's wave breathes (amplitude modulates on a 5-second cycle);
inactive waves hold static.

**Bundled with the prototype:** a live configuration panel with 12 sliders
that tunes every parameter — wave shape, carousel proportions, light
intensity, grain — in real time. The tuner is the killer feature for reuse:
drop into a new project, drag sliders, bake new defaults, remove tuner.

## When to use it
- ✓ Hero sections that need to present 2–4 distinct entry points with
  emotional weight (each "door" is a portal to a sub-experience)
- ✓ Wellness, healing, contemplative, or premium brands where pace matters
- ✓ When you want continuous, calm motion (breathing wave + drifting lights)
  rather than literal animation that feels anxious
- ✗ Speed/efficiency-focused product sites — the slow rotation works against urgency
- ✗ Content-dense pages — the carousel needs 400vh of dedicated scroll budget
- ✗ Sites where multiple heroes / scroll-driven sections coexist (don't stack
  two 400vh sticky sections on one page)

## What it depends on
- Vanilla JS (no framework). Canvas 2D API. SVG with `<clipPath>`.
- Modern browser features: CSS `aspect-ratio`, `dvh`, custom properties, `perspective`
- Browser support: evergreen browsers (Chrome 108+, Safari 15.4+, Firefox 101+)
- SVG `<image>` with `clipPath` using `clipPathUnits="userSpaceOnUse"`
- Parent of `.hub` (the carousel container) must have `overflow: hidden` so side
  arches that translate off-screen don't create horizontal scrollbars

## How to integrate (3 steps)
1. **Copy the HTML structure** for the hub (canvas, stage with 3 arches,
   info-stack, dot rail) into your page. Prefix all class names (e.g. `wp-`
   for wellness portal) to avoid collisions with your site's existing styles.
2. **Copy the `<style>` block and `<script>` IIFE**. Update CSS class
   selectors and JS DOM IDs to match your prefix.
3. **Open the tuner**, adjust to your brand's feel, then bake the chosen
   values into the `cfg` object and remove the tuner panel from production.

## Gotchas
- **Mobile media queries that set `.arch { width: Xvw }`** will fight the
  JS-driven sizing and produce square elements that crop top/bottom via
  `preserveAspectRatio`. Don't add such overrides — let JS size for all viewports.
- **`overflow: hidden` on the stage** (not the hub) chops the dome and wave
  when arch sizing is off by even 1px. Apply `overflow: hidden` only at the
  hub level, not the stage.
- **`preserveAspectRatio="slice"` on the SVG** crops top/bottom on aspect
  mismatch. Use `meet` for defensive safety — only the path is shown, never cropped.
- **Wave amplitude must exceed Breath amp**, otherwise
  `liveAmp = amp + sin(...) × breathAmp` can dip to 0 or negative, making the
  wave appear flat at certain moments in the breath cycle.
- **Global film grain (`body::before` at z-index 50)** can double up with any
  section-specific grain layer. Use one or the other, never both — the
  multiply blend composites them and the result is too dark.
- **400vh scroll wrapper** monopolizes scroll budget. Don't stack two
  scroll-driven hero sections on one page.
- **SVG `<image>` element needs `preserveAspectRatio="xMidYMid slice"`**
  (separate from the parent SVG's preserveAspectRatio) so the photo fills the
  arch shape with cover behavior.

## Locked defaults (production-approved 2026-05-24, army-pink wellness portal)

| Group | Parameter | Value | Notes |
|---|---|---|---|
| Wave | Amplitude | `5` | px in viewBox space |
| Wave | Frequency | `2.1` | full cycles across arch bottom |
| Wave | Speed | `0.017` | phase advance per frame |
| Wave | Breath amp | `2.5` | must stay ≤ Amplitude |
| Wave | Breath cycle | `5s` | breath modulation period |
| Carousel | Fill ratio | `92%` | of stage height |
| Carousel | Spread | `46vw` | side door translation from center |
| Carousel | Tilt | `5°` | subtle 3D rotation (Y-axis) |
| Carousel | Side scale | `0.59` | side door size as fraction of center |
| Backdrop | Light intensity | `0.55` | opacity of drifting cream lights |
| Backdrop | Light size | `0.6` | radius as fraction of `max(w, h)` |
| Backdrop | Grain opacity | `0.3` | "letterpress" feel — see grain-texture pattern |

## Where it came from
Built for Army Pink's wellness portal hero (2026-05-23 to 2026-05-24).
Inspired by:
- Daylight Computer's WebGL drifting-light backdrops (canvas-2d approximation here)
- Apple Cover Flow / iOS Stories peeking carousel
- Roman arches + meditation studio aesthetics
- Wei's "step into a room" framing for the wellness portal entry experience

## Open questions / things to reconsider
- **Mobile gesture layer**: currently no horizontal swipe — desktop and
  mobile use the same vertical-scroll-rotation. Worth adding swipe for mobile.
- **Reduced-motion fallback**: needs implementation.
  `prefers-reduced-motion: reduce` should disable carousel rotation and
  breathing wave, show all 3 doors statically side by side.
- **The tuner panel itself** could be extracted as its own pattern
  (`live-tuner-overlay` or similar) — it's reusable across very different
  visual experiments. Promote to its own library entry once used in a 2nd context.
- **The wave-arch SVG path generator** (`buildArchPath()`) could be its own
  pattern (`arch-with-animated-wave`). It's already reused for static arches
  in other Army Pink sections.
- **Sub-pages** (Calm Room, Library, Wellness Experiences) — the door CTAs
  currently `preventDefault` because the routes don't exist. Wire to real
  routes once built.
