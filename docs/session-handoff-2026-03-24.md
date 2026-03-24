# Session Handoff — March 24, 2026

## Current State of the Portfolio

### Live URL
https://angevalenti.github.io/ange-portfolio/

### Repo
github.com/angevalenti/ange-portfolio

### Design System (Finalized)
- **Teal**: #014744 (primary accent — buttons, links, emphasis)
- **Blush**: #FBE9E1 (warm accent — stat bars, Challenge band, credentials band, scalloped edges)
- **Gold**: #D49D00 (detail accent — labels, highlights, stat bar labels)
- **Deep Blush**: #B07868 (text highlight accent)
- **Black**: #1A1A16 (body text, headings)
- **Cream Nav**: #F5F0EB (nav bar, Overview section backgrounds, Technical Details bg)
- **Fonts**: Fraunces weight 300 (headlines, italic emphasis) + Inter weight 400 (body)
- **Signature details**: Blush scalloped edges (Challenge band, stat bar, About page, homepage credentials band)

### Site Structure (SPA — all in index.html)
- **Homepage** (#page-home): Centered circular photo with blush offset shadow, "INSTRUCTIONAL DESIGNER & EDUCATOR" subtitle, name with gold period, tagline quote ("Educator by training, designer by nature."), teal View Work button (blush on hover), blush credentials band with scalloped edge above dark footer
- **Portfolio** (#page-portfolio): Minimal editorial list with colored circles (per-project accent colors), category tags, Fraunces italic titles
- **About** (#page-about): Philosophy quote at top → scalloped edge → blush WHO I AM section (photo left, bio right, skill pills) → scalloped edge → white contact stat bar (Email, LinkedIn, Available For, Focus) → dark footer
- **Contact**: Merged into About page — no separate contact page

### Nav
HOME · PORTFOLIO · ABOUT (no Contact)
Angela *Valenti* — Fraunces weight 300, last name italic

### Project Pages (6 total, all in projects/)
All use the unified template: warm cream nav → white hero (text left, image right) → blush stat bar with scalloped top → cream Overview → blush scalloped Challenge band (side-by-side layout) → white Approach → cream Technical Details → dark footer with "Next project →"

| # | File | Project | Accent Color | Launch Course Links To |
|---|------|---------|-------------|----------------------|
| 01 | project-template.html | Language Through Film | #014744 | lessons/pursuit_of_happyness_interactive_lesson.html |
| 02 | whats-next.html | Discover Your Direction | #2D6A5E | lessons/whats-next-v2.html |
| 03 | esl-lesson.html | Identity, Language & Belonging | #4A7C6F | lessons/grade2_esl_lesson_wida5.html |
| 04 | ready_for_whats_next_case_study.html | Ready for What's Next | #1B6B6B | lessons/ready_for_whats_next.html |
| 05 | raising_humans.html | Raising Humans in the Age of Algorithms | #2E4057 | raising_humans_course.html |
| 06 | study-buddies.html | Study Buddies | #C8956C | #lessons (anchor to lesson cards section) |

### Study Buddies Lesson Cards (3 lessons, each with unique color)
- Lesson 01: Circulatory System — #C25B56 (warm red)
- Lesson 02: Respiratory System — #5B8FA8 (soft blue)
- Lesson 03: The 13 Colonies — #8B7355 (warm brown)

### Case Study Content (all written in grounded, natural voice)
All 6 project pages have real copy:
- **Top 3 (deep case studies)**: Language Through Film, Ready for What's Next, Study Buddies
- **Supporting 3 (lighter copy)**: Discover Your Direction, Identity Language & Belonging, Raising Humans

### About Page Bio (current text)
"I'm an instructional designer with a background most people in this field don't have — K–12 classroom experience in ESL and Special Education, a BA in Graphic Design, and a hands-on comfort with HTML, CSS, and JavaScript that lets me build what I design.

Most designers specialize. I generalize on purpose. The best learning experiences don't come from handing a storyboard to a developer and hoping it comes back right. They come from one person who understands the learner, the content, and the build — and can move between all three.

Every project in this portfolio was designed and built by me, using AI as a development partner. I make the creative calls — the look, the structure, the pedagogy. AI helps me write the code and move faster. The result is work that would normally take a team, done by one person who cares about every detail."

### Skills Listed
Instructional Design · Curriculum Development · ESL/ELL · K-12 · WIDA · UDL · HTML/CSS/JS · Graphic Design · Figma · Adobe Creative Suite · GitHub · AI-Assisted Development

## Next Session Priorities
1. **Audit stat bars and titles** — make sure each project's stat bar data and hero titles are accurate and consistent with the About page skills/credentials
2. **Build out new project features** — Ange plans to enhance existing projects
3. **Add real screenshots** — hero image placeholders still need actual project screenshots on most pages (Language Through Film has some added to Challenge section)

## Dev Environment
- Launch CC: `cd ~/Documents/Portfolio && claude --dangerously-skip-permissions`
- Local preview: `python3 -m http.server 8000` (sometimes needs `kill $(lsof -ti:8000)` first)
- Push live: `git add -A && git commit -m "message" && git push origin main`
- Live site updates ~60 seconds after push
- Hard refresh: Cmd+Shift+R to see changes

## Workflow Reminder
- **Ange** = Creative Director — all design/content decisions
- **Claude (chat)** = Strategist — writes CC prompts in copy-paste blocks
- **Claude Code (CC)** = Builder — executes all code
- Always preview before pushing when making big changes
- Git verify: `git ls-files [filepath]` to confirm files are tracked
