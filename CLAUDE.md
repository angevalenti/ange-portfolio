# CLAUDE.md — Angela Valenti Portfolio

## Project Overview

Personal portfolio website for Angela Valenti, an instructional designer and K–12 educator
transitioning into full-time instructional design and e-learning development. The site is
a single-page application (SPA) built with vanilla HTML/CSS/JS, designed for deployment
on GitHub Pages. Navigation between sections is handled by a `showPage()` function that
toggles a `.active` class on `<div class="page">` containers — no routing library.

---

## Site Owner

**Angela Valenti**
- Instructional Designer / E-Learning Developer
- PA-certified K–12 educator: ESL, Visual Art, Special Education
- BA in Graphic Design
- Based in Pennsylvania, USA · Available remote
- LinkedIn: linkedin.com/in/angelavalenti

---

## Deployment & Dev

| | |
|---|---|
| GitHub repo | https://github.com/angevalenti/ange-portfolio.git |
| GitHub Pages URL | https://angevalenti.github.io/ange-portfolio/ |
| Local dev server | `python3 -m http.server 8000` → http://localhost:8000 |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5, semantic elements |
| Styles | Vanilla CSS with custom properties (`--var`), no preprocessor |
| Scripts | Vanilla JavaScript (ES6), no frameworks or libraries |
| Fonts | Google Fonts CDN — Cormorant Garamond + DM Sans |
| Images | JPEGs for photos, SVGs for placeholders |
| Deployment target | GitHub Pages (static, no server) |
| Build system | None — direct file editing |

---

## Aesthetic & Style Guide

### Philosophy
Editorial / luxury print aesthetic — inspired by high-end print design (Kinfolk, Wallpaper*).
The visual language is intentionally restrained: near-monochrome palette, strong typographic
hierarchy, deliberate rule lines and grid discipline, with a single electric accent color as
the sole departure from restraint. Aesthetics are treated as part of the instructional content,
not decoration — reflected in the site's own philosophy quote: *"Aesthetics aren't separate
from learning. They're part of it."*

### Color Palette

| Variable | Hex | Usage |
|---|---|---|
| `--black` | `#0e0e0e` | Near-black: text, dark panels, nav |
| `--white` | `#f8f8f4` | Warm off-white: page background |
| `--mid` | `#6a6a6a` | Medium gray: body copy, labels, muted UI |
| `--accent` | `#c8f000` | Electric chartreuse: hover fills, CTAs, contact panel, footer highlight |
| `--accent-dark` | `#9ab800` | Olive-yellow: borders, active nav underline, accent hover state |
| `--rule` | `#e0e0dc` | Light warm gray: all dividing lines, card borders |

The chartreuse (`--accent`) is used sparingly and intentionally — hover states on project
rows, the "Download" button, the entire contact left panel, the last hero stat card, and
the footer logo italic. It should never appear decoratively; every use is structural or
interactive.

### Typography

| Variable | Font | Weights Used | Role |
|---|---|---|---|
| `--font-display` | Cormorant Garamond, Georgia, serif | 300, 400, 600; italic variants | Headlines, name, project titles, large numerals, stat numbers |
| `--font-body` | DM Sans, sans-serif | 300, 400, 500, 700 | Nav, body copy, labels, buttons, form fields |

**Key typographic conventions:**
- Display font always at weight 300 (light) except the logo mark (600)
- Italic is used structurally: last name in hero, taglines, `<em>` in headlines
- Body labels run at 0.62–0.72rem with `letter-spacing: 0.12–0.2em` and `text-transform: uppercase`
- `clamp()` used throughout for fluid responsive sizing
- `-webkit-font-smoothing: antialiased` applied globally
- Line heights: 0.88–0.95 for large display text, 1.75–1.85 for body copy

### Spacing & Layout Conventions
- Nav height: `--nav-h: 64px` (fixed, used as offset everywhere)
- Section padding: `5rem 3rem` desktop → `3rem 1.5rem` mobile
- Grid gaps use `1px` with `background: var(--rule)` on the grid container to create hairline separators (portfolio grid)
- Easing: `--ease: cubic-bezier(0.4, 0, 0.2, 1)`

### Animation
Two named keyframes, used sparingly:
- `fadeUp`: `opacity 0 → 1` + `translateY(18px → 0)`, staggered across hero elements
- `fadeIn`: `opacity 0 → 1`, used on the hero rule line

### Recurring Visual Motifs
- **Ghost/watermark text**: Large near-transparent serif text as decorative background (hero `::before` shows "AV", about section shows "AV", portfolio cards show card numbers)
- **Chartreuse accent square**: A `48×48px` solid `--accent` block used as a decorative geometric element (color strip, hero photo corner offset)
- **Hairline rules**: `1px solid var(--rule)` dividers everywhere — between sections, inside grids, flanking the hero mid-row
- **Uppercase tracked labels**: Small-caps-style labels in DM Sans with wide letter-spacing precede nearly every content block

---

## Site Structure

After the Step 1–6 refactor, the site has 4 pages + footer:

```
index.html
│
├── #page-home (default active)
│   ├── Hero — full-viewport: kicker / name / [tagline | photo | desc+CTA] / stats bar
│   ├── Color strip — black band with philosophy quote
│   └── Selected Work — numbered list of 3 featured projects (links to Portfolio page)
│
├── #page-portfolio
│   └── Portfolio — filterable 3-col grid, 6 cards
│       Filters: All · E-Learning · Curriculum · Design
│       Cards: project-1.svg → project-6.svg (placeholders)
│       Live link: project-pursuit.html (card 01 only)
│
├── #page-about
│   └── About — 2-col split
│       Left: black panel, "AV" ghost text, portrait photo
│       Right: kicker / headline / bio / skill tags / quick-facts table
│
├── #page-contact
│   └── Contact — 2-col split
│       Left: chartreuse panel, large CTA text, contact info
│       Right: contact form (Name, Email, Subject, Message)
│              Note: form has no backend — submit fakes success visually
│
└── footer
    └── Logo · nav links · copyright
```

### Asset Paths
```
assets/
├── css/
│   └── styles.css          — all styles, ~540 lines, single source of truth
├── fonts/                  — stub, empty (Google Fonts loaded via CDN)
├── images/
│   ├── hero-photo.jpg      — hero section portrait (141KB)
│   ├── about-photo.jpg     — about section portrait (58KB)
│   ├── project-1.svg       — portfolio card 01 placeholder
│   ├── project-2.svg       — portfolio card 02 placeholder
│   ├── project-3.svg       — portfolio card 03 placeholder
│   ├── project-4.svg       — portfolio card 04 placeholder
│   ├── project-5.svg       — portfolio card 05 placeholder
│   └── project-6.svg       — portfolio card 06 placeholder
└── js/                     — stub, empty (all JS is inline in index.html <script>)
```

---

## Current Status

- [x] Directory structure created for GitHub Pages
- [x] CSS extracted from inline `<style>` to `assets/css/styles.css`
- [x] CSS deduplicated — 3x duplicate blocks removed, unused hero variants removed
- [x] Photos extracted from base64 to real JPEG files
- [x] Resume page removed (nav link, page div, footer link, and all CSS)
- [x] SVG placeholder thumbnails in place for all 6 portfolio cards
- [ ] Contact form has no real backend (fakes submit visually)
- [ ] Only 1 of 6 portfolio project pages exists (`project-pursuit.html`)
- [ ] No meta description or OG/social sharing tags
- [ ] `portfolio-v2.html` backup still exists at root (safe to delete when ready)

---

## Next Steps

- TODO: Wire contact form to a real backend — Formspree (`action="https://formspree.io/f/..."`) or Netlify Forms (`netlify` attribute) are both zero-server options compatible with GitHub Pages
- TODO: Create project detail pages for cards 02–06; replace SVG placeholders with real screenshots when available
- TODO: Add `<meta name="description">` and Open Graph tags (`og:title`, `og:description`, `og:image`) to `<head>` in index.html
- TODO: Add a `favicon.ico` or `<link rel="icon">` — currently none
- TODO: Move inline JS from `<script>` block in index.html to `assets/js/main.js` and add `<script src="assets/js/main.js" defer></script>`
- TODO: Delete `portfolio-v2.html` from root once refactor is confirmed stable
- TODO: Add `404.html` for GitHub Pages (optional but recommended for SPA-style nav)
- TODO: Verify mobile layout on real devices — responsive CSS was rationalized in this refactor but not device-tested
