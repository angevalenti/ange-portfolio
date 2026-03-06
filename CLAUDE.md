# CLAUDE.md — Angela Valenti Portfolio

## 1. Project Overview

Personal portfolio website for Angela Valenti — instructional designer, K–12 educator, and e-learning developer. The site is a single-page application (SPA) built with vanilla HTML/CSS/JS and deployed on GitHub Pages.

- **Live site:** https://angevalenti.github.io/ange-portfolio/
- **Repo:** https://github.com/angevalenti/ange-portfolio (private)
- Navigation is handled by `showPage()`, which toggles `.active` on `<div class="page">` containers — no routing library

The site has 4 SPA pages (Home, Portfolio, About, Contact) plus standalone project case study pages in the `projects/` folder.

---

## 2. The Team & How We Work

**Ange (Angela Valenti) — Creative Director & Decision-Maker**
- Has final say on all design, content, and scope decisions
- Never start a big build without confirming direction with her first
- When in doubt, ask — don't assume

**Claude (chat session) — Strategist & Prompt Writer**
- Lives in claude.ai chat
- Translates Ange's direction into structured prompts for Claude Code
- Does not write code directly

**Claude Code (CC) — Builder**
- Executes all technical implementation
- Takes prompts from the chat session and builds from them
- Asks when direction is unclear
- Never makes design or content assumptions without confirmation

---

## 3. Local Preview Workflow

- **Local server:** `python3 -m http.server 8000` from `~/Documents/Portfolio/`
- **Preview at:** http://localhost:8000
- Always preview changes locally before pushing to GitHub
- CC should not push to GitHub until Ange confirms the preview looks good

---

## 4. GitHub & Deployment

| | |
|---|---|
| Repo | https://github.com/angevalenti/ange-portfolio |
| GitHub Pages | https://angevalenti.github.io/ange-portfolio/ |
| Default branch | `main` |
| CLI tool | `gh` (GitHub CLI) |

- Use `gh` CLI for authentication when pushing
- Commit messages should be descriptive and session-specific
- Do not push without Ange's approval

---

## 5. File & Folder Structure

```
Portfolio/
├── index.html                          — SPA shell (Home, Portfolio, About, Contact)
├── assets/
│   ├── css/
│   │   └── styles.css                  — All shared styles, single source of truth
│   └── images/
│       ├── bookscopy.jpg               — Hero photo (homepage)
│       ├── headshot-2.jpg              — About page photo
│       ├── high-school-minority.png    — Card 01 thumbnail
│       ├── future-careers.png          — Card 02 thumbnail
│       └── 2nd-grader-working.png      — Card 03 thumbnail
├── projects/
│   ├── project-template.html           — Case study: Language Through Film (card 01)
│   ├── whats-next.html                 — Case study: Discover Your Direction (card 02)
│   ├── esl-lesson.html                 — Case study: Identity, Language & Belonging (card 03)
│   ├── ready_for_whats_next_case_study.html  — Case study: Ready for What's Next (card 04)
│   ├── project_handoff.html            — Session handoff doc for Ready for What's Next
│   └── lessons/
│       ├── pursuit_of_happyness_interactive_lesson.html
│       ├── whats-next-v2.html
│       ├── grade2_esl_lesson_wida5.html
│       └── esl_lesson_template.html
└── portfolio-v2.html                   — Old backup, safe to delete
```

---

## 6. Design System

### Portfolio Shell (index.html + project case study pages)
- **Background:** `#F8F7F2` off-white / `#F8F4F4` cream sections
- **Black:** `#0e0e0e`
- **Mid gray:** `#6a6a6a`
- **Rule:** `#e0e0dc`
- **Accent:** `#FF6B81` (pink-coral) — featured tags, decorative elements, eyebrows on dark sections
- **Display font:** Fraunces, weight 300; italic for elegance
- **Body font:** Inter (updated from DM Sans in recent sessions)
- **Nav height:** 64px fixed

### Case Study Pages
- Use `esl-lesson.html` as the exact structural template
- Each project has its own accent color:
  - `project-template.html` (Language Through Film): `#FF6B81`
  - `whats-next.html` (Discover Your Direction): `#FF6B81`
  - `esl-lesson.html` (Identity, Language & Belonging): `#FF6B81`
  - `ready_for_whats_next_case_study.html` (Ready for What's Next): `#1B6B6B` deep teal
- Case study CSS lives inline in each project page `<style>` block
- Shared styles come from `../assets/css/styles.css`

### Portfolio Grid
- Filters: All · E-Learning (visible to user)
- Cards 01–04 are visible; cards 05–09 have `data-hidden` and `style="display:none"`
- Filter JS uses `:not([data-hidden])` to prevent revealing hidden cards

---

## 7. Session Log — What Was Built

### Session — March 2026 (Current)
- Redesigned About page (`#page-about`) — dark hero, cream bio section with smaller photo, dark philosophy pull quote, facts strip
- Redesigned Contact page (`#page-contact`) — removed heavy chartreuse left panel, single centered column, warm personal paragraph, clean contact rows
- Removed Philosophy section from homepage entirely
- Updated hero photo to `bookscopy.jpg` with `filter: none`
- Added `#FF6B81` period after "Valenti." in hero heading
- Renamed portfolio card titles: Language Through Film · Discover Your Direction · Identity, Language & Belonging
- Made portfolio card thumbnails clickable links to project overview pages
- Color updates: `#217a7a` on email and LinkedIn links (about + contact pages)
- Built `projects/ready_for_whats_next_case_study.html` — case study page matching `esl-lesson.html` template, accent color `#1B6B6B`
- Added Ready for What's Next as card 04 in portfolio grid (visible, `data-cat="curriculum"`)
- `project_handoff.html` already existed in `projects/` folder — not modified

### Earlier Sessions
- Git initialized, connected to GitHub, GitHub Pages enabled
- CSS extracted from inline styles to `assets/css/styles.css`
- All 3 existing project case study pages redesigned with new layout system (ps-section--light / ps-section--dark pattern)
- Portfolio thumbnails added for cards 01–03
- Cards 04–08 hidden with `data-hidden`; filter simplified to All + E-Learning
- Base64 photos extracted to JPEG files in `assets/images/`
- Resume page removed entirely

---

## 8. Known To-Do

- Contact form has no real backend (display only)
- No `<meta name="description">` or Open Graph tags
- No favicon
- `portfolio-v2.html` at root can be deleted
- No `404.html` for GitHub Pages SPA navigation
- Mobile layout not yet device-tested
