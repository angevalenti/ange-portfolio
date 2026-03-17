# Session Handoff — March 17, 2026
**Prepared by: Ange + Claude**

---

## Team & Workflow
- **Ange** = Creative Director — drives all design and content decisions
- **Claude (chat)** = Strategist & Prompt Writer — never writes code directly; crafts prompts in copy-paste code blocks
- **Claude Code (CC)** = Builder — executes all technical work, reads files before editing, surgical changes only
- **Flow:** strategize in chat → Claude writes prompt → Ange pastes into CC → CC builds → Ange reports back → iterate

---

## Dev Environment
- **Terminal:** zsh
- **CC launch:** `cd ~/Documents/Portfolio && claude --dangerously-skip-permissions`
- **Local server:** `python3 -m http.server 8000` → http://localhost:8000
- **GitHub repo:** github.com/angevalenti/ange-portfolio
- **Live site:** https://angevalenti.github.io/ange-portfolio
- **GitHub Pages:** deploys from `main` branch
- **Git tip:** always verify new images with `git ls-files [filepath]` before assuming they're deployed

---

## Portfolio Site — Current State

### Design
- **Palette:** `#F8F4F4` cream background · `#B07A8A` / `#8C5F6E` mauve tones · `#FF6B81` coral accent
- **Typography:** Fraunces (display, weight 300, italic) + Inter (body)
- **Aesthetic:** editorial, elegant, restrained — not corporate

### Pages
| File | Route | Notes |
|------|-------|-------|
| `index.html` | SPA shell | Home, Portfolio, About, Contact all live here |
| `projects/project-template.html` | Card 01 case study | Language Through Film |
| `projects/whats-next.html` | Card 02 case study | Discover Your Direction |
| `projects/esl-lesson.html` | Card 03 case study | Identity, Language & Belonging |
| `projects/ready_for_whats_next_case_study.html` | Card 04 case study | Ready for What's Next |
| `projects/raising_humans.html` | Card 05 — live project page | Raising Humans in the Age of Algorithms |

### Portfolio Grid — Visible Cards
| # | Title | Thumbnail | Link | Category |
|---|-------|-----------|------|----------|
| 01 | Language Through Film | `high-school-minority.png` | `projects/project-template.html` | E-Learning |
| 02 | Discover Your Direction | `future-careers.png` | `projects/whats-next.html` | E-Learning |
| 03 | Identity, Language & Belonging | `2nd-grader-working.png` | `projects/esl-lesson.html` | Curriculum |
| 04 | Ready for What's Next | `high-school-senior.png` | `projects/ready_for_whats_next_case_study.html` | Curriculum |
| 05 | Raising Humans in the Age of Algorithms | `a-teenager-with-a-dream.png` | `projects/raising_humans.html` | E-Learning |

### Hidden / Inactive Cards
| # | Title | Status |
|---|-------|--------|
| 05 (dup) | Visual Arts Curriculum | `data-hidden`, no project page |
| 06 | Instructional Media | `data-hidden`, no project page |
| 06 | Graphic Design Portfolio | `data-hidden`, no project page |
| 07 | Township Connect App | `data-hidden`, no project page |

### About Page
- Split layout: dark hero section + cream bio section with smaller photo
- Philosophy pull quote in dark band
- Facts/credentials strip

---

## Project: Ready for What's Next
**File:** `projects/lessons/ready_for_whats_next.html`
**Case study:** `projects/ready_for_whats_next_case_study.html`

### What's Built
- 5-unit interactive e-learning module for high school seniors
- **Unit topics:**
  1. Digital Identity — accent `#A78BFA`
  2. AI Tools & You — accent `#00D4FF`
  3. Money & Digital Life — accent `#FB7185`
  4. Workplace Communication — accent `#A855F7`
  5. College & Career Portals — accent `#4ADE80`

### Build Status
- **Phase 1 — Design Tokens:** Complete — full `:root` CSS custom property token system, Manrope + IBM Plex Sans font swap
- **Phase 2 — Component Alignment:** Complete — coral CTA buttons, quiz radio indicators, accordion left-accent borders, progress bar gradient, pull quotes, unit card shadows, footer
- **Phase 3 — Accessibility:** Complete — skip link, landmark roles, focus rings, reduced motion, quiz ARIA (`radiogroup`/`radio`/`aria-checked`), accordion ARIA, dark mode contrast verified
- **Multilingual:** EN / ES / RU (Portuguese removed)
- **Light/dark mode toggle:** functional, defaults to light mode
- **Lesson nav footer:** sticky bottom bar — Previous Unit / Save for Later / Mark Complete — localStorage persistence
- **Resource cards:** dark cards inside each unit linking to downloadable resources

### Downloadable Resources (`projects/lessons/resources/`)
| File | Type | Unit |
|------|------|------|
| `unit1_online_presence_map.html` | Worksheet | Unit 1 — Digital Identity |
| `unit2_ai_detective_game.html` | Activity Guide | Unit 2 — AI Tools & You |
| `unit3_financial_checklist.html` | Interactive Checklist | Unit 3 — Money & Digital Life |
| `unit4_communication_checklist.html` | Interactive Checklist | Unit 4 — Workplace Communication |
| `unit5_career_portal_guide.html` | Activity Guide | Unit 5 — College & Career Portals |

All 5 resources have: Print/PDF buttons, `@media print` styles, back-to-course link, Manrope + IBM Plex Sans, responsive layout.

---

## Project: Raising Humans in the Age of Algorithms
**File:** `projects/raising_humans.html`
**Live on portfolio:** Card 05, visible

### What's Built
- 8-unit parent education course on child development and technology
- **Fonts:** Manrope + IBM Plex Sans (aligned to design system)
- **All 5 infographics complete:** Brain Timeline, Screen Time Stats, Age-by-Age Table, Algorithm Funnel, Mental Health Trend Line
- Neon per-unit accent colors with glow effects
- Dark bands for pull quotes and Research Says callouts
- Stat card rows, scroll-progress indicator, live quiz score tracker
- **Thumbnail:** `a-teenager-with-a-dream.png`
- Pushed live with thumbnail

### Build Status
- Full content complete; no design token / accessibility pass done yet (same treatment Ready for What's Next received is queued for this project)

---

## Design System
**File:** `docs/course-design-system.md` (2,557 lines)

8-part buildable reference document:
1. Design Foundations
2. Component Library
3. Page Templates (7 types)
4. Interaction Patterns
5. Accessibility Standards
6. Responsive Framework
7. Gap Analysis
8. Quickstart Checklist

Derived from Stitch prototype screenshots + audit of both existing projects. A browsable React artifact was also built in chat (not a file in this repo).

---

## What's In Progress / Next Up

### 1. Project Page Template Redesign (Approved, Not Started)
- **Current problem:** oversized hero, buried content
- **Approved direction — Option C:**
  - Full-bleed screenshot hero with gradient overlay
  - Stats strip below hero
  - Zigzag staggered 2-column (text left / screenshot right, alternating)
- Apply to ALL project overview pages
- **Blocker:** needs course screenshots to implement

### 2. Homepage Layout / Grid Redesign
- On the list, not yet started

### 3. About Page Polish
- On the list, not yet started

### 4. Raising Humans Design Pass
- Not started
- Same design token / component alignment / accessibility treatment that Ready for What's Next received

---

## Git Log (most recent 15 commits)
```
148617e Ready for What's Next redesign — design tokens, component alignment, accessibility pass, 5 downloadable resources
036a6b4 Add Raising Humans thumbnail
be43a47 Fix portfolio — single Raising Humans card, remove Stitch export
c6780d1 Remove Stitch prototype export — design system spec captured separately
85acea1 Raising Humans — font swap, infographic placeholders, prep for live
c33fcad Add raising_humans parent ed course — full content, design system, infographics, font update
9d0f319 Fix card 04 thumbnail and add card 05 image
40aa869 Update CLAUDE.md with session log and team workflow documentation
837e269 Add light/dark mode toggle with CSS variables and sun/moon pill button
07d0f42 Add multilingual toggle (EN/ES/PT/RU), accessibility pass, and fix lesson launch link
03ce101 Update CLAUDE.md with session log and team workflow
ba20fdc Add Ready for What's Next case study page and portfolio card
fc5f754 Redesign about page, remove philosophy from homepage, update contact page, color and typography updates
149d6cd Redesign project template layout, update headshot to grayscale
08f4471 Fix filter to only show projects 01-03, simplify to E-Learning category
```

---

## Assets — `assets/images/`
| File | Used For |
|------|----------|
| `bookscopy.jpg` | Hero photo — homepage |
| `headshot-2.jpg` | About page photo |
| `headshot.jpg` | Older headshot (unused) |
| `high-school-minority.png` | Card 01 thumbnail — Language Through Film |
| `future-careers.png` | Card 02 thumbnail — Discover Your Direction |
| `2nd-grader-working.png` | Card 03 thumbnail — Identity, Language & Belonging |
| `high-school-senior.png` | Card 04 thumbnail — Ready for What's Next |
| `a-teenager-with-a-dream.png` | Card 05 thumbnail — Raising Humans |
| `a-teenager-with-a-dream-of-a-job.png` | Raising Humans alt variant |
| `a-teenager-with-a-dream-of-a-job (1).png` | Raising Humans alt variant |
| `high-school-seniors.png` | Unused or alt |
| `high-school-esl-class.png` | Unused or alt |
| `future-high-school-graduates-careers.png` | Unused or alt |
| `elementary-school-2nd-graders-at-the-whiteboard-in.png` | Hidden card — Visual Arts Curriculum |
| `2nd-graders-working.png` | Unused or alt |
| `2nd-graders-working-at-the-board.png` | Unused or alt |
| `web-app-for-township-garbage-collection.png` | Hidden card — Township Connect App |
| `brand-identity.png` | Unused or alt |
| `IMG_5530-EDIT.jpg` | Unused |
| `IMG_9140.jpg` | Unused |
| `books.jpg` | Unused (older hero?) |
| `pexels-karola-g2-6375.jpg` | Unused |
| `thinkdifferently.jpg` | Unused |
| `do good.jpg` | Unused |
| `project-1.svg` – `project-6.svg` | SVG placeholders (legacy) |
| `Angela Valenti — Resume.html` | Resume export — **NOT git-tracked, intentional** |
| `Angela Valenti — Resume.pdf` | Resume export — **NOT git-tracked, intentional** |
| `Angela Valenti — Resume_files/` | Resume export folder — **NOT git-tracked, intentional** |

---

## Known Issues / Gotchas
- **Resume files** (`Angela Valenti — Resume.html`, `.pdf`) are in `assets/images/` but intentionally NOT git-tracked — do not add them
- **Git tracking:** always verify new images with `git ls-files [filepath]` before assuming they're deployed
- **CC context limits:** long build sessions hit limits; queue targeted continuation prompts before session ends
- **Browser cache:** `Cmd+Shift+R` after every push, or test in incognito
- **Contact form:** no real backend — display only
- **No `<meta>` / Open Graph tags** on any page
- **No favicon**
- **`portfolio-v2.html`** at root — safe to delete, never has been
- **No `404.html`** for GitHub Pages SPA navigation
- **Mobile layout** not yet device-tested
- **Card numbering quirk:** there are two cards labeled "05" in the grid — one visible (Raising Humans), one hidden (Visual Arts Curriculum) — if cards are ever un-hidden, numbering will need cleanup
