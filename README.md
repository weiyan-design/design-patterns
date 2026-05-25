# Design Pattern Library

Reusable visual patterns harvested from real projects. Each pattern is
documented, demonstrated by a runnable `example.html`, and ready to drop into
a new project.

**The bouncer rule:** a pattern only enters the library after it's been used
in 2+ projects *or* is unambiguously general. One-offs stay in the project
that birthed them. This single rule kills ~70% of junk before it accumulates.

**Before integrating any visual pattern into a new project, read this index
first** to see if something already exists. Avoid re-inventing what's here.

**Live demos**: every pattern includes a runnable `example.html`. The full
collection is hosted via GitHub Pages at
**https://weiyan-design.github.io/design-patterns/** — click any "demo" link
in the table below to open the pattern in your browser.

---

## Patterns

| Pattern | Status | Demo | What it does | Tags |
|---|---|---|---|---|
| [grain-texture](grain-texture/) | production | [▶ live](https://weiyan-design.github.io/design-patterns/grain-texture/example.html) | Body-wide film-grain noise overlay via `body::before` | texture, global, css-only, no-js |
| [coverflow-doors-tuner](coverflow-doors-tuner/) | experiment | [▶ live](https://weiyan-design.github.io/design-patterns/coverflow-doors-tuner/example.html) | 3-door scroll-driven coverflow carousel with arch wave + live config tuner | layout, hero, carousel, svg, canvas, animation, scroll-driven, 3d |

---

## Adding a new pattern

**The easiest way:** invoke the `add-design-pattern` skill in any Claude
Code session. Say "add this to my design library" (or `/add-design-pattern`)
and Claude walks through every step below, enforces the bouncer rule, fills
the template from conversation context, commits, pushes, and confirms the
live URL. The skill lives at `~/.claude/skills/add-design-pattern/SKILL.md`
and is versioned in the `weiyan-design/claude-config` repo.

**Manual steps** (what the skill automates):

1. **Apply the bouncer rule.** Has this pattern been used in 2+ projects, or
   is it clearly general? If no, leave it in the project — don't extract yet.
2. **Create a folder** named in kebab-case. Name describes *what* it is, not
   what it looks like. (`arch-with-wavy-bottom`, not `cool-archy-thing`.)
3. **Copy `_TEMPLATE.md`** into the folder as `README.md`. Fill in every
   section. If you can't fill a section, the pattern isn't ready to extract.
4. **Drop in `example.html`** — a standalone, runnable demo. No build step,
   no external deps. Double-click to view locally, or open the live URL on
   GitHub Pages once pushed.
5. **Record `preview.mp4`** (or `preview.gif`) — 5–15 seconds showing the
   pattern in motion. For static patterns, a `preview.png` is fine.
6. **Add a row to the table above** with a `▶ live` demo link. Status
   starts at `experiment`; promote to `production` after a second successful
   reuse. Live URL format:
   `https://weiyan-design.github.io/design-patterns/<pattern-name>/example.html`
7. **Commit & push.** The repo is public with GitHub Pages enabled — the
   live URL works the moment the commit hits `main` (~60s for first build).
   No pattern is considered "added" until the live URL is confirmed.

---

## Repo + hosting

- **Repo:** [weiyan-design/design-patterns](https://github.com/weiyan-design/design-patterns) (public)
- **Local path:** `~/Documents/Vibe Code/_design-library/`
- **Live demos:** [weiyan-design.github.io/design-patterns/](https://weiyan-design.github.io/design-patterns/) (GitHub Pages from `main` at root)
- **Skill:** `add-design-pattern` (lives in `~/.claude/skills/`, versioned in `weiyan-design/claude-config`)

---

## Status meanings

- **production** — battle-tested, used in 1+ shipped projects, no known surprises
- **experiment** — promising but unproven; safe to grab, expect adjustments
- **archived** — kept for reference but superseded or stale; don't use without revisiting

Patterns move between statuses over time. Promote experiments that proved
out. Demote production patterns that haven't been used in 12+ months. Archive
what's truly dead — but never delete (you might want it back).

---

## Quarterly hygiene

Every ~3 months: re-read this index. Check each pattern's `last-touched`
date. Update statuses. This is the moment that prevents the library from
rotting into a junk drawer.
