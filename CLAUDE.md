# CLAUDE.md — Portfolio Project Documentation

## Team Roles
- **Ange (Creative Director):** Makes all design and content decisions. Drives the creative vision.
- **Claude (Strategist + Prompt Writer):** Strategizes in claude.ai chat. Writes all CC prompts in copy-paste code blocks. Never writes code directly.
- **Claude Code (Builder):** Executes all technical work. Reads files before editing. Makes surgical changes only.

## How We Work
1. Ange and Claude strategize in claude.ai chat
2. Claude writes a prompt in a copy-paste code block
3. Ange pastes the prompt into Claude Code
4. CC builds and reports back
5. Ange reviews and reports results back to Claude
6. Iterate until done
7. Commit in batches using: git add -A

## Local Development
- Local preview server: http://localhost:8000
- Always preview changes at localhost:8000 before committing
- Launch dev environment: cd ~/Documents/Portfolio then claude --dangerously-skip-permissions in zsh
- Always confirm new image files are tracked with: git ls-files [filepath]
- Do not push to GitHub until Ange confirms she is ready

## Project Overview
- **Portfolio site:** angevalenti.github.io/ange-portfolio
- Fonts: Fraunces (display) + Inter (body)
- Palette: #B07A8A, #8C5F6E, #F8F4F4, accent #FF6B81
- Three live project tiles: Language Through Film, Discover Your Direction, Identity Language & Belonging
- Two hidden tiles ready to activate: Township Connect App, Super Super

- **Ready for What's Next module:** projects/lessons/ready_for_whats_next.html
- Five units: Digital Identity, AI Tools & You, Money & Digital Life, Workplace Communication, College & Career Portals
- Per-unit accent colors: Unit 1 #A78BFA, Unit 2 #00D4FF, Unit 3 #FB7185, Unit 4 #A855F7, Unit 5 #4ADE80
- Features: animated unit cards, accordion content, one-question-at-a-time quiz, progress bar

## File & Folder Structure

```
Portfolio/
├── index.html                                    — SPA shell (Home, Portfolio, About, Contact)
├── assets/
│   ├── css/
│   │   └── styles.css                            — All shared styles, single source of truth
│   └── images/
│       ├── bookscopy.jpg                         — Hero photo (homepage)
│       ├── headshot-2.jpg                        — About page photo
│       ├── high-school-minority.png              — Card 01 thumbnail
│       ├── future-careers.png                    — Card 02 thumbnail
│       ├── 2nd-grader-working.png                — Card 03 thumbnail
│       └── high-school-senior.png                — Card 04 thumbnail (Ready for What's Next)
├── projects/
│   ├── project-template.html                     — Case study: Language Through Film (card 01)
│   ├── whats-next.html                           — Case study: Discover Your Direction (card 02)
│   ├── esl-lesson.html                           — Case study: Identity, Language & Belonging (card 03)
│   ├── ready_for_whats_next_case_study.html      — Case study: Ready for What's Next (card 04)
│   └── lessons/
│       ├── ready_for_whats_next.html             — Interactive lesson module (main)
│       ├── pursuit_of_happyness_interactive_lesson.html
│       ├── whats-next-v2.html
│       ├── grade2_esl_lesson_wida5.html
│       └── esl_lesson_template.html
└── portfolio-v2.html                             — Old backup, safe to delete
```

## Design System

### Portfolio Shell (index.html + project case study pages)
- **Background:** `#F8F7F2` off-white / `#F8F4F4` cream sections
- **Black:** `#0e0e0e`
- **Mid gray:** `#6a6a6a`
- **Rule:** `#e0e0dc`
- **Accent:** `#FF6B81` (pink-coral) — featured tags, decorative elements, eyebrows on dark sections
- **Display font:** Fraunces, weight 300; italic for elegance
- **Body font:** Inter
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
- Cards 01–04 are visible; cards 05+ have `data-hidden` and `style="display:none"`
- Filter JS uses `:not([data-hidden])` to prevent revealing hidden cards

## Session Log

### Session — March 10, 2026
- Completed multilingual toggle (EN/ES/PT/RU) with sticky flag pill UI top-right
- Completed accessibility pass: ARIA labels, keyboard nav, ✓/✗ quiz indicators
- Fixed Russian translations — fully parallel to EN/ES/PT
- Fixed lesson launch link on Ready for What's Next case study page
- Added light/dark mode toggle with sun/moon pill button (top-left), CSS variables
- Added high-school-senior.png thumbnail to Ready for What's Next project card
- Wired thumbnail image as a live link to the case study page
- Pushed all changes to GitHub Pages

### Session — March 2026 (Earlier)
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

### Earlier Sessions
- Git initialized, connected to GitHub, GitHub Pages enabled
- CSS extracted from inline styles to `assets/css/styles.css`
- All 3 existing project case study pages redesigned with new layout system (ps-section--light / ps-section--dark pattern)
- Portfolio thumbnails added for cards 01–03
- Cards 04+ hidden with `data-hidden`; filter simplified to All + E-Learning
- Base64 photos extracted to JPEG files in `assets/images/`
- Resume page removed entirely

## Known To-Do
- Contact form has no real backend (display only)
- No `<meta name="description">` or Open Graph tags
- No favicon
- `portfolio-v2.html` at root can be deleted
- No `404.html` for GitHub Pages SPA navigation
- Mobile layout not yet device-tested
