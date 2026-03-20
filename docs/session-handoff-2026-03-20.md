# Session Handoff — March 20, 2026

## What Was Built

### Circulatory System Lesson (`projects/lessons/circulatory_system.html`)
- **Status**: Complete, live
- 2,107 lines, single-file HTML, vanilla JS
- 9 sections: cells, tissues, cell theory timeline, cell organelles (9 interactive hotspots), circulatory overview, blood vessels (drag-and-match quiz), 4-chamber heart diagram, step-by-step blood flow animation, 8-question final quiz
- Design: Fredoka + Nunito, comic-book energy, bold reds/blues/pinks, hard drop shadows
- Features: drag-to-order, scroll animations (IntersectionObserver), confetti, floating score badge, responsive

### Respiratory System Lesson (`projects/lessons/respiratory_system.html`)
- **Status**: Complete, minor polish possible
- ~1,700+ lines, single-file HTML, vanilla JS
- 8 sections: respiratory basics, interactive organ diagram (8 hotspots), breathing mechanics + "Breathe Along" exercise, 7-stop animated oxygen journey, alveoli zoom + gas exchange mini-game, respiratory+circulatory teamwork cycle diagram, fun fact flip cards, 10-question final quiz
- Design: Baloo 2 + Quicksand, teal/sky-blue/coral "Breath of Fresh Air" palette, glassmorphism cards, wave SVG dividers
- Features: Web Audio API (9 sounds, default ON), canvas particle system (O₂/CO₂), flip cards, scroll progress bar, score badge, responsive
- **Polish items for later**:
  - Section 2 body diagram SVG could be more anatomically polished
  - Fun facts cards — SVG illustration replacements + bigger answer text (was in progress)
  - General polish pass

### Study Buddies Project Page (`projects/study-buddies.html`)
- **Status**: Complete, live
- Overview/case study page following existing portfolio structure
- Accent color: #C8956C (warm amber)
- Links to both lesson files via "Launch Lesson" buttons
- "Coming Soon" strip mentioning the Operation game
- Tile 06 on homepage grid is wired up and pointing here

### Operation Game (`projects/lessons/operation_game.html`)
- **Status**: NOT BUILT — CC hit 32k token limit on first attempt
- **To build**: Set `export CLAUDE_CODE_MAX_OUTPUT_TOKENS=64000` before starting
- **Build plan**: Split into Pass 1 (respiratory mode only, playable) + Pass 2 (add circulatory + full body modes)
- Design: "Operating Room Neon" dark theme, Lilita One + Nunito, neon glows, crosshair cursor
- Mechanics: Clue cards → click correct organ on body SVG → extraction animation. 3 lives, 15-sec timer, scoring + star rating
- Full Pass 1 prompt is ready (ask chat Claude for it)

## Next Session: Portfolio Design System

Focus: design system consistency across the portfolio shell (NOT the course/lesson design system).

### Potential areas:
- Homepage grid redesign
- About page polish
- Project page template redesign (Option C was selected previously but Ange wanted a genuinely new direction — follow-up questions about pain points and preferred vibe were unanswered)
- Raising Humans design pass
- Navigation and overall site cohesion
- Typography/color/spacing consistency

### Portfolio shell design tokens:
- Fonts: Fraunces (display) + Inter (body)
- Colors: mauve #B07A8A, dark mauve #8C5F6E, cream #F8F4F4, accent #FF6B81
- Per-project accents on tiles (amber for Study Buddies, etc.)

## Standing Reminders
- Three-role system: Ange = Creative Director, Chat Claude = Strategist/Prompt Writer, CC = Builder
- All prompts in copy-paste code blocks, no editing needed
- Git: `git add -A`, commit in batches, verify images with `git ls-files`
- Dev: `cd ~/Documents/Portfolio && claude --dangerously-skip-permissions`
- Local preview: `python3 -m http.server 8000`
- Browser cache: Cmd+Shift+R or incognito after pushing
- CC context limits: break big builds into sequential passes
