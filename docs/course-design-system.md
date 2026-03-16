# Course Design System Specification
**Raising Humans in the Age of Algorithms — and all future courses**
*Version 1.0 — March 2026*

---

## How to Use This Document

This is a buildable reference, not a style guide. Every section contains real CSS values, HTML patterns, and class conventions derived from two sources: (1) the Raising Humans Stitch prototype screenshots and (2) a full audit of the two existing course projects (`ready_for_whats_next.html` and `raising_humans.html`). Jump to any section independently — each is self-contained.

**Screenshot references:** `[S1]` Unit Intro · `[S2]` Lesson Page · `[S3]` Quiz View · `[S4]` Quiz Results · `[S5]` Interactive Checklist · `[S6]` Worksheet · `[S7]` Activity Guide

---

# PART 1: DESIGN FOUNDATIONS

## 1.1 Design Philosophy

> "Good design isn't just beautiful — it's accessible, intentional, and built for every learner in the room."
> — Angela Valenti

Four operating principles that every course should embody:

1. **Research-backed authority without coldness.** These courses carry real academic weight. The design earns trust through precision (tight type, clean grids, cited stats) but stays warm through illustration, personal voice, and encouraging feedback.
2. **Every element earns its place.** No decoration without purpose. Colored borders signal unit identity. Icon badges signal topic category. Gradient progress bars signal forward momentum. If it's there, it means something.
3. **Print and digital are equal citizens.** Worksheets, checklists, and activity guides must look as intentional on paper as they do on screen. Design for both from the start.
4. **One-at-a-time learning reduces cognitive load.** Quizzes reveal one question at a time. Accordions hold content until opened. The sidebar holds supporting material so the main column stays focused.

---

## 1.2 Design Token System

Implement as CSS custom properties on `:root`. Override per-project or per-unit by scoping to a class or data attribute.

### Base Color Palette

```css
:root {
  /* ── Backgrounds ── */
  --color-bg-dark:        #0B0B12;   /* deep navy — dark hero sections */
  --color-bg-mid:         #151520;   /* slightly lighter navy — dark cards */
  --color-bg-light:       #F6F7F8;   /* near-white — page bg, quiz bg */
  --color-bg-white:       #FFFFFF;   /* pure white — lesson pages, worksheet */
  --color-bg-overlay:     rgba(8, 8, 15, 0.85); /* hero image overlay */

  /* ── Text ── */
  --color-text-primary:   #1A1A2E;   /* near-black — all body/heading text on light */
  --color-text-secondary: #4A4A6A;   /* medium gray-blue — supporting text */
  --color-text-muted:     #8888A0;   /* muted — labels, captions, meta */
  --color-text-inverse:   #F0F0F5;   /* near-white — text on dark backgrounds */
  --color-text-inverse-secondary: #A0A0B2; /* on dark, secondary */

  /* ── Borders ── */
  --color-border-light:   #E5E7EB;   /* light page dividers */
  --color-border-dark:    #2A2A3C;   /* borders in dark sections */
  --color-border-card:    rgba(0, 0, 0, 0.08); /* subtle card border */

  /* ── Primary Action (Coral) ── */
  --color-coral:          #FF5C3A;   /* primary CTA — "Mark Complete", checklist headers */
  --color-coral-light:    #FFF0ED;   /* tinted bg for coral callouts */
  --color-coral-dark:     #E04020;   /* hover/pressed state */

  /* ── Semantic / Feedback ── */
  --color-correct:        #22C55E;   /* quiz correct */
  --color-incorrect:      #EF4444;   /* quiz incorrect */
  --color-correct-bg:     rgba(34, 197, 94, 0.10);
  --color-incorrect-bg:   rgba(239, 68, 68, 0.08);
  --color-correct-text:   #16A34A;
  --color-incorrect-text: #DC2626;

  /* ── Callout Card Backgrounds ── */
  --color-pro-tip-bg:     #FFF4EE;   /* peach — Pro-Tip card [S5, S7] */
  --color-milestone-bg:   #FFF0EC;   /* light salmon — Next Milestone card [S5] */
  --color-alert-bg:       #101a22;   /* dark — Critical Alert card [S1] */

  /* ── Shadows ── */
  --shadow-card:    0 2px 20px rgba(0, 0, 0, 0.07);
  --shadow-card-lg: 0 8px 32px rgba(0, 0, 0, 0.12);
  --shadow-inset:   inset 0 0 0 1px rgba(0, 0, 0, 0.06);
}
```

### Per-Unit Accent System

Each unit gets two accent colors. Assign on the unit's container element:

```css
/* Pattern: set on .unit-section, .unit-view, or [data-unit="N"] */

[data-unit="1"] {
  --unit-accent:   #00F5FF;   /* cyan */
  --unit-accent2:  #CCFF00;   /* acid yellow */
  --unit-accent-rgb: 0, 245, 255;
}
[data-unit="2"] {
  --unit-accent:   #FF2D78;   /* hot pink */
  --unit-accent2:  #FF6B00;   /* electric orange */
  --unit-accent-rgb: 255, 45, 120;
}
[data-unit="3"] {
  --unit-accent:   #FFE600;   /* neon yellow */
  --unit-accent2:  #FF4D4D;   /* hot coral-red */
  --unit-accent-rgb: 255, 230, 0;
}
[data-unit="4"] {
  --unit-accent:   #39FF14;   /* neon green */
  --unit-accent2:  #0066FF;   /* electric blue */
  --unit-accent-rgb: 57, 255, 20;
}
/* Units 5–8 cycle through the same pairs */
[data-unit="5"] { --unit-accent: #FF2D78; --unit-accent2: #FF6B00; --unit-accent-rgb: 255, 45, 120; }
[data-unit="6"] { --unit-accent: #00F5FF; --unit-accent2: #CCFF00; --unit-accent-rgb: 0, 245, 255; }
[data-unit="7"] { --unit-accent: #39FF14; --unit-accent2: #0066FF; --unit-accent-rgb: 57, 255, 20; }
[data-unit="8"] { --unit-accent: #FFE600; --unit-accent2: #FF4D4D; --unit-accent-rgb: 255, 230, 0; }
```

To apply an accent as a subtle tinted background:
```css
background: rgba(var(--unit-accent-rgb), 0.08);
border-left: 4px solid var(--unit-accent);
```

### Spacing Scale

```css
:root {
  --space-1:   4px;
  --space-2:   8px;
  --space-3:   12px;
  --space-4:   16px;
  --space-5:   20px;
  --space-6:   24px;
  --space-8:   32px;
  --space-10:  40px;
  --space-12:  48px;
  --space-16:  64px;
  --space-20:  80px;
}
```

### Border Radius Scale

```css
:root {
  --radius-sm:   4px;    /* small badges, tags */
  --radius-md:   8px;    /* cards, quiz buttons */
  --radius-lg:   12px;   /* main content cards */
  --radius-xl:   16px;   /* hero cards, featured blocks */
  --radius-pill: 9999px; /* pill badges, CTA buttons */
}
```

### Transition Tokens

```css
:root {
  --transition-fast:   150ms ease;
  --transition-base:   250ms ease;
  --transition-slow:   400ms ease;
  --transition-spring: 300ms cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

---

## 1.3 Typography System

### Font Pairing Strategy

**Slot 1 — Display (headings, hero text, pull quotes):** `Manrope`
- Used in: `raising_humans.html`, all Stitch prototype pages
- Why: Extra-bold weight (800) creates the authoritative impact visible in screenshots; optical rounding at large sizes feels approachable, not corporate
- Fallback: `system-ui, -apple-system, sans-serif`

**Slot 2 — Body (paragraphs, UI labels, form elements):** `IBM Plex Sans`
- Used in: `raising_humans.html`, Stitch worksheet/checklist pages
- Why: Clean, slightly technical feel reinforces the research-backed tone; highly legible at small sizes; pairs with Manrope without competing
- Fallback: `Inter, system-ui, sans-serif`

```html
<!-- Google Fonts import — include on every course page -->
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&family=IBM+Plex+Sans:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
```

```css
:root {
  --font-display: 'Manrope', system-ui, sans-serif;
  --font-body:    'IBM Plex Sans', Inter, system-ui, sans-serif;
}

body {
  font-family: var(--font-body);
  font-size: 1rem;
  line-height: 1.75;
  color: var(--color-text-primary);
  -webkit-font-smoothing: antialiased;
}
```

### Heading Hierarchy

```css
/* H1 — Hero/page titles */
h1, .text-h1 {
  font-family: var(--font-display);
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 800;
  line-height: 1.1;
  letter-spacing: -0.02em;
  color: var(--color-text-primary);
}

/* H2 — Section headers */
h2, .text-h2 {
  font-family: var(--font-display);
  font-size: clamp(1.5rem, 3.5vw, 2.1rem);
  font-weight: 800;
  line-height: 1.2;
  letter-spacing: -0.015em;
}

/* H3 — Card/component titles */
h3, .text-h3 {
  font-family: var(--font-display);
  font-size: 1.1rem;
  font-weight: 700;
  line-height: 1.35;
}

/* H4 / Eyebrow — Labels, category names */
h4, .text-h4 {
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  line-height: 1.4;
}
```

### Eyebrow / Label Pattern

The single most repeated typographic element across all 7 page types:

```css
.eyebrow {
  display: inline-block;
  font-family: var(--font-body);
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--unit-accent, var(--color-coral));
  margin-bottom: var(--space-3);
}

/* Pill variant — visible in [S3] "MODULE ASSESSMENT", [S7] "UNIT 1: DIGITAL WELLNESS" */
.eyebrow--pill {
  background: rgba(var(--unit-accent-rgb, 255, 92, 58), 0.10);
  color: var(--unit-accent, var(--color-coral));
  padding: 4px 10px;
  border-radius: var(--radius-pill);
}

/* Inverse variant — on dark backgrounds */
.eyebrow--inverse {
  color: var(--unit-accent);
  opacity: 0.9;
}
```

### Body Text Scale

```css
.text-lead   { font-size: 1.15rem; line-height: 1.75; }  /* hero subtitles */
.text-body   { font-size: 1rem;    line-height: 1.75; }  /* standard paragraphs */
.text-body-sm{ font-size: 0.975rem;line-height: 1.8;  }  /* accordion body, checklist */
.text-sm     { font-size: 0.875rem;line-height: 1.6;  }  /* support text, captions */
.text-xs     { font-size: 0.78rem; line-height: 1.5;  }  /* labels, meta */
.text-micro  { font-size: 0.72rem; line-height: 1.4;  }  /* footer, legal, mini badges */
```

---

## 1.4 Iconography & Visual Elements

### Colored Icon Badge [S2, S5, S7]

Circular badge with icon, colored by topic. Used on "How it Works" cards and activity cards.

```css
.icon-badge {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(var(--unit-accent-rgb), 0.12);
  color: var(--unit-accent);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.icon-badge--lg {
  width: 56px;
  height: 56px;
  font-size: 1.4rem;
}

/* Numbered step badge [S7] */
.step-badge {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: var(--unit-accent);
  color: var(--color-bg-dark);
  font-family: var(--font-display);
  font-weight: 800;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
```

### Decorative Quotation Marks [S2, S7]

Large typographic marks, not images. Positioned behind quote text.

```css
.pull-quote {
  position: relative;
}

.pull-quote::before {
  content: '\201C';  /* opening curly quote */
  font-family: var(--font-display);
  font-size: 6rem;
  font-weight: 800;
  line-height: 1;
  color: var(--color-coral);
  opacity: 0.25;
  position: absolute;
  top: -0.5rem;
  left: -0.5rem;
  pointer-events: none;
}
```

### Unit Number Badge [S1]

```css
.unit-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 12px;
  border-radius: var(--radius-pill);
  background: var(--unit-accent);
  color: var(--color-bg-dark);
  font-family: var(--font-body);
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
```

### Checkbox Style [S5, S6]

```css
.checkbox-item {
  display: flex;
  gap: var(--space-4);
  align-items: flex-start;
}

.checkbox-box {
  width: 22px;
  height: 22px;
  border-radius: var(--radius-sm);
  border: 2px solid var(--color-border-light);
  flex-shrink: 0;
  cursor: pointer;
  transition: background var(--transition-fast), border-color var(--transition-fast);
  display: flex;
  align-items: center;
  justify-content: center;
}

.checkbox-box.checked {
  background: var(--unit-accent);
  border-color: var(--unit-accent);
  color: var(--color-bg-dark);
}
```

### Progress Indicators

```css
/* Thin progress bar — sticky course progress strip [S2] */
.progress-bar-track {
  height: 4px;
  background: var(--color-border-light);
  border-radius: var(--radius-pill);
  overflow: hidden;
}

.progress-bar-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--unit-accent), var(--unit-accent2));
  border-radius: var(--radius-pill);
  transition: width 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

/* Quiz question progress dots [S3] */
.progress-dots {
  display: flex;
  gap: 6px;
  align-items: center;
}

.progress-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--color-border-light);
  transition: background var(--transition-fast);
}

.progress-dot.active { background: var(--unit-accent); }
.progress-dot.complete { background: var(--color-correct); }

/* Circular progress ring — quiz results [S4] */
/* Implemented via SVG, see Quiz Results template */
```

---

# PART 2: COMPONENT LIBRARY

---

## [CORE] Navigation Bar

**Purpose:** Top-of-page course branding and navigation. Two visual variants.

**Variant A — Course Nav** [S2, S5, S7]: Light bg, logo left, nav links center/right, user avatar or action buttons far right.

```html
<header class="course-nav" role="banner">
  <div class="course-nav__brand">
    <div class="course-nav__logo" aria-hidden="true">
      <!-- icon or initials -->
    </div>
    <div class="course-nav__name">
      <span class="course-nav__course-title">Raising Humans</span>
      <span class="course-nav__unit-label">Unit 2: The Early Years</span>
    </div>
  </div>
  <nav class="course-nav__links" aria-label="Course navigation">
    <a href="#">Modules</a>
    <a href="#">Resources</a>
  </nav>
  <div class="course-nav__actions">
    <!-- export/print buttons, avatar, or quiz exit button -->
  </div>
</header>
```

**Variant B — Quiz Nav** [S3]: Minimal. Brand left, current unit center, Exit Quiz button right.

**Variant C — Resource Nav** [S6, S7]: Brand left only, action buttons (Print / PDF / Download) far right.

```css
.course-nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 var(--space-6);
  height: 60px;
  background: var(--color-bg-white);
  border-bottom: 1px solid var(--color-border-light);
  position: sticky;
  top: 0;
  z-index: 100;
}

.course-nav__brand {
  display: flex;
  align-items: center;
  gap: var(--space-3);
}

.course-nav__logo {
  width: 32px;
  height: 32px;
  border-radius: var(--radius-md);
  background: linear-gradient(135deg, var(--unit-accent), var(--unit-accent2));
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-bg-dark);
  font-weight: 800;
  font-size: 0.85rem;
}

.course-nav__course-title {
  font-family: var(--font-display);
  font-weight: 800;
  font-size: 0.95rem;
  color: var(--color-text-primary);
}

.course-nav__unit-label {
  display: block;
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--color-text-muted);
}

.course-nav__links {
  display: flex;
  gap: var(--space-6);
}

.course-nav__links a {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--color-text-secondary);
  text-decoration: none;
  transition: color var(--transition-fast);
}

.course-nav__links a:hover { color: var(--color-text-primary); }
```

**Accessibility:** `role="banner"`, `aria-label` on `<nav>`, active page indicated with `aria-current="page"`.

---

## [CORE] Lesson Progress Strip

**Purpose:** Thin bar directly below nav showing unit/lesson position and completion %. [S2]

```html
<div class="progress-strip" role="status" aria-label="Lesson progress">
  <div class="progress-strip__label">
    <span>Unit 2 | Lesson 4 of 12</span>
  </div>
  <div class="progress-strip__bar">
    <div class="progress-strip__fill" style="width: 33%" aria-hidden="true"></div>
  </div>
  <div class="progress-strip__pct">33% Complete</div>
</div>
```

```css
.progress-strip {
  display: flex;
  align-items: center;
  gap: var(--space-4);
  padding: 6px var(--space-6);
  background: var(--color-bg-white);
  border-bottom: 1px solid var(--color-border-light);
}

.progress-strip__label {
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--color-text-muted);
  white-space: nowrap;
}

.progress-strip__bar {
  flex: 1;
  height: 4px;
  background: var(--color-border-light);
  border-radius: var(--radius-pill);
  overflow: hidden;
}

.progress-strip__fill {
  height: 100%;
  background: linear-gradient(90deg, var(--unit-accent), var(--unit-accent2));
  border-radius: var(--radius-pill);
  transition: width 0.6s ease;
}

.progress-strip__pct {
  font-size: 0.75rem;
  font-weight: 700;
  color: var(--unit-accent);
  white-space: nowrap;
}
```

---

## [CORE] Stat Card Row

**Purpose:** Row of 3–4 key data points with icon, label, large metric, and source. [S1]

```html
<div class="stat-row" role="list">
  <div class="stat-card" role="listitem">
    <div class="stat-card__icon" aria-hidden="true"><!-- icon --></div>
    <div class="stat-card__label eyebrow">Global Avg</div>
    <div class="stat-card__value">7.5 hrs</div>
    <div class="stat-card__desc">Daily screen interaction for ages 8–12</div>
  </div>
  <!-- repeat -->
</div>
```

```css
.stat-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: var(--space-4);
  margin: var(--space-8) 0;
}

.stat-card {
  padding: var(--space-6);
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-left: 4px solid var(--unit-accent);
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
  box-shadow: var(--shadow-card);
}

.stat-card__value {
  font-family: var(--font-display);
  font-size: 2rem;
  font-weight: 800;
  line-height: 1.1;
  color: var(--color-text-primary);
  margin: 4px 0;
}

.stat-card__desc {
  font-size: 0.82rem;
  color: var(--color-text-secondary);
  line-height: 1.5;
}

/* Critical Alert variant — dark [S1] */
.stat-card--alert {
  background: var(--color-alert-bg);
  border-left-color: var(--color-coral);
  color: var(--color-text-inverse);
}

.stat-card--alert .stat-card__label { color: var(--color-coral); }
.stat-card--alert .stat-card__desc  { color: var(--color-text-inverse-secondary); }
```

---

## [CORE] CTA Buttons

```css
/* Primary — coral/salmon fill [S2, S5] */
.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  padding: 14px 28px;
  background: linear-gradient(135deg, var(--color-coral), var(--color-coral-dark));
  color: #FFFFFF;
  font-family: var(--font-body);
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.04em;
  border: none;
  border-radius: var(--radius-pill);
  cursor: pointer;
  text-decoration: none;
  transition: opacity var(--transition-fast), transform var(--transition-fast);
}

.btn-primary:hover {
  opacity: 0.9;
  transform: translateY(-1px);
}

/* Accent primary — uses unit accent color [S3] */
.btn-accent {
  background: var(--unit-accent);
  color: var(--color-bg-dark);
}

/* Dark filled [S4] "Continue to Unit" */
.btn-dark {
  background: var(--color-bg-dark);
  color: var(--color-text-inverse);
  font-family: var(--font-display);
  font-size: 0.85rem;
  font-weight: 800;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border-radius: var(--radius-pill);
  padding: 16px 32px;
  border: none;
  cursor: pointer;
  transition: background var(--transition-fast);
}

/* Outlined [S4] "Review Unit" */
.btn-outline {
  background: transparent;
  color: var(--color-text-primary);
  border: 2px solid var(--color-border-light);
  border-radius: var(--radius-pill);
  padding: 14px 28px;
  font-family: var(--font-display);
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  cursor: pointer;
  transition: border-color var(--transition-fast), background var(--transition-fast);
}

.btn-outline:hover {
  border-color: var(--color-text-primary);
  background: rgba(0,0,0,0.02);
}

/* Ghost — print/export style [S6, S7] */
.btn-ghost {
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-md);
  padding: 8px 16px;
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--color-text-secondary);
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  text-decoration: none;
  transition: border-color var(--transition-fast), color var(--transition-fast);
}

.btn-ghost:hover {
  border-color: var(--color-text-primary);
  color: var(--color-text-primary);
}
```

**Accessibility:** All buttons use `<button>` or `<a>` with visible text. Icon-only buttons require `aria-label`. Disabled state: `aria-disabled="true"`, `opacity: 0.4`.

---

## [CORE] Pull Quote

**Purpose:** Highlights a key expert statement. Appears in dark or light variants. [S2, S7]

```html
<blockquote class="pull-quote">
  <p>"These simple interactions are the literal building blocks of brain architecture."</p>
  <footer class="pull-quote__attribution">
    <cite>— Center on the Developing Child</cite>
  </footer>
</blockquote>
```

```css
/* Light variant [S2] */
.pull-quote {
  position: relative;
  padding: var(--space-10) 0;
  border-top: 1px solid var(--color-border-light);
  border-bottom: 1px solid var(--color-border-light);
}

.pull-quote::before {
  content: '\201C';
  font-family: var(--font-display);
  font-size: 8rem;
  font-weight: 800;
  color: var(--color-coral);
  opacity: 0.2;
  position: absolute;
  top: var(--space-4);
  left: -1rem;
  line-height: 1;
  pointer-events: none;
  user-select: none;
}

.pull-quote p {
  font-family: var(--font-display);
  font-size: clamp(1.3rem, 3vw, 1.8rem);
  font-weight: 700;
  font-style: italic;
  line-height: 1.4;
  color: var(--color-text-primary);
  max-width: 720px;
  padding-left: 2rem;
}

.pull-quote__attribution {
  margin-top: var(--space-5);
  padding-left: 2rem;
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--color-text-muted);
  display: flex;
  align-items: center;
  gap: var(--space-4);
}

.pull-quote__attribution::before {
  content: '';
  display: block;
  width: 32px;
  height: 2px;
  background: var(--unit-accent);
}

/* Dark variant [S7] */
.pull-quote--dark {
  background: var(--color-bg-dark);
  border-radius: var(--radius-lg);
  padding: var(--space-10) var(--space-8);
  border-top: none;
  border-bottom: none;
}

.pull-quote--dark p    { color: var(--color-text-inverse); }
.pull-quote--dark::before { color: var(--unit-accent); opacity: 0.3; }
.pull-quote--dark .pull-quote__attribution { color: var(--color-text-inverse-secondary); }
```

---

## [CORE] Standard Content Card

```html
<div class="content-card">
  <div class="icon-badge" aria-hidden="true"><!-- icon --></div>
  <h3 class="content-card__title">1. Notice the Serve</h3>
  <p class="content-card__body">Pay attention to where the child is looking or what they are pointing at.</p>
</div>
```

```css
.content-card {
  padding: var(--space-6);
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.content-card__title {
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 700;
  color: var(--color-text-primary);
}

.content-card__body {
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  line-height: 1.65;
}
```

---

## [CORE] Section Container (Light / Dark Band)

```css
/* Light content band */
.section-light {
  background: var(--color-bg-white);
  padding: var(--space-16) 0;
}

/* Dark content band */
.section-dark {
  background: var(--color-bg-dark);
  padding: var(--space-16) 0;
  color: var(--color-text-inverse);
}

/* Tinted accent band */
.section-tinted {
  background: rgba(var(--unit-accent-rgb), 0.05);
  padding: var(--space-12) 0;
  border-top: 1px solid rgba(var(--unit-accent-rgb), 0.15);
  border-bottom: 1px solid rgba(var(--unit-accent-rgb), 0.15);
}

/* Shared inner container */
.section-inner {
  max-width: 860px;
  margin: 0 auto;
  padding: 0 var(--space-6);
}

.section-inner--wide {
  max-width: 1200px;
}
```

---

## [RECOMMENDED] "What You'll Learn" Objectives List

```html
<section class="objectives-section" aria-labelledby="objectives-heading">
  <h2 id="objectives-heading" class="eyebrow">What You'll Learn</h2>
  <ul class="objectives-list" role="list">
    <li class="objectives-item">
      <div class="icon-badge" aria-hidden="true">🧠</div>
      <div>
        <h3 class="objectives-item__title">Neural Plasticity Basics</h3>
        <p class="objectives-item__desc">How the developing brain rewires itself in response to digital stimuli.</p>
      </div>
    </li>
  </ul>
</section>
```

```css
.objectives-list {
  list-style: none;
  padding: 0;
  margin: var(--space-6) 0 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-5);
}

.objectives-item {
  display: flex;
  gap: var(--space-4);
  align-items: flex-start;
}

.objectives-item__title {
  font-weight: 700;
  font-size: 0.95rem;
  margin-bottom: 2px;
}

.objectives-item__desc {
  font-size: 0.875rem;
  color: var(--color-text-secondary);
  line-height: 1.6;
}
```

---

## [RECOMMENDED] "Try This Today" Sidebar Card

**Purpose:** Action-oriented sidebar card on lesson pages. Dark background, checklist items, download link. [S2]

```html
<aside class="try-today-card" aria-label="Try This Today actions">
  <div class="try-today-card__header">
    <span aria-hidden="true">🚀</span>
    <h3>Try This Today</h3>
  </div>
  <ul class="try-today-card__list" role="list">
    <li class="try-today-card__item">
      <span class="try-today-card__check" aria-hidden="true">✓</span>
      <span><strong>Narrate your day:</strong> Describe what you're doing while cooking or cleaning.</span>
    </li>
  </ul>
  <a href="#" class="try-today-card__download btn-ghost btn-ghost--inverse" download>
    <span aria-hidden="true">↓</span> Download Quick Guide
  </a>
</aside>
```

```css
.try-today-card {
  background: #1A1F2E;
  border-radius: var(--radius-xl);
  padding: var(--space-6);
  color: var(--color-text-inverse);
  display: flex;
  flex-direction: column;
  gap: var(--space-5);
}

.try-today-card__header {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 800;
}

.try-today-card__list {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

.try-today-card__item {
  display: flex;
  gap: var(--space-3);
  font-size: 0.875rem;
  line-height: 1.6;
  color: var(--color-text-inverse-secondary);
}

.try-today-card__check {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: var(--color-coral);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.65rem;
  flex-shrink: 0;
  margin-top: 2px;
}

.try-today-card__download {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: 12px;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: var(--radius-md);
  color: var(--color-text-inverse);
  font-size: 0.82rem;
  font-weight: 600;
  text-decoration: none;
  transition: background var(--transition-fast);
}

.try-today-card__download:hover {
  background: rgba(255,255,255,0.10);
}
```

---

## [RECOMMENDED] "Need Help?" Support Card

```html
<div class="support-card">
  <h4 class="support-card__heading">Need Help?</h4>
  <p class="support-card__body">Chat with our specialists if you have questions about this lesson.</p>
  <a href="#" class="support-card__link">Open Support Chat ↗</a>
</div>
```

```css
.support-card {
  padding: var(--space-5) var(--space-6);
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-lg);
}

.support-card__heading {
  font-family: var(--font-display);
  font-size: 0.95rem;
  font-weight: 700;
  margin-bottom: var(--space-2);
}

.support-card__body {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
  margin-bottom: var(--space-3);
  line-height: 1.6;
}

.support-card__link {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--unit-accent, var(--color-coral));
  text-decoration: none;
}
```

---

## [RECOMMENDED] Instructor Badge

**Purpose:** Attribution for content author. [S5, S6]

```html
<div class="instructor-badge">
  <img class="instructor-badge__avatar" src="[avatar.jpg]" alt="Photo of Dr. Sarah Chen" width="44" height="44">
  <div>
    <div class="instructor-badge__label eyebrow">Instructor</div>
    <div class="instructor-badge__name">Dr. Sarah Chen</div>
  </div>
</div>
```

```css
.instructor-badge {
  display: flex;
  align-items: center;
  gap: var(--space-4);
  padding: var(--space-3) var(--space-5);
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-lg);
  width: fit-content;
}

.instructor-badge__avatar {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  object-fit: cover;
}

.instructor-badge__name {
  font-family: var(--font-display);
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--color-text-primary);
}
```

---

## [RECOMMENDED] Pro-Tip Callout Card

**Purpose:** Warm peach card with practical insight. Appears at bottom of checklists and guides. [S5, S7]

```html
<div class="pro-tip-card" role="note" aria-label="Pro Tip">
  <div class="pro-tip-card__header">
    <span aria-hidden="true">📍</span>
    <span class="eyebrow">Pro-Tip</span>
  </div>
  <p>"The most important thing is to be present. You don't need fancy toys — just your attention."</p>
</div>
```

```css
.pro-tip-card {
  background: var(--color-pro-tip-bg);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.pro-tip-card__header {
  display: flex;
  align-items: center;
  gap: var(--space-2);
}

.pro-tip-card p {
  font-style: italic;
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  line-height: 1.65;
}
```

---

## [RECOMMENDED] Next Milestone Card

**Purpose:** Salmon card showing what unlocks next. [S5]

```html
<div class="milestone-card">
  <div class="milestone-card__header">
    <span aria-hidden="true">📅</span>
    <span class="eyebrow" style="color: var(--color-coral)">Next Milestone</span>
  </div>
  <div class="milestone-card__title">Unit 3: The Impact of Toxic Stress</div>
  <div class="milestone-card__unlock">Unlock next Tuesday at 9:00 AM</div>
</div>
```

```css
.milestone-card {
  background: var(--color-milestone-bg);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  border-left: 3px solid var(--color-coral);
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.milestone-card__title {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 0.95rem;
  color: var(--color-text-primary);
}

.milestone-card__unlock {
  font-size: 0.82rem;
  color: var(--color-text-muted);
}
```

---

## [RECOMMENDED] Topic Performance Bar

**Purpose:** Per-topic score visualization in quiz results. [S4]

```html
<div class="perf-bar" role="meter" aria-label="Neural Pathway Formation: 100%"
     aria-valuenow="100" aria-valuemin="0" aria-valuemax="100">
  <div class="perf-bar__header">
    <span class="perf-bar__label">Neural Pathway Formation</span>
    <span class="perf-bar__pct">100%</span>
  </div>
  <div class="perf-bar__track" aria-hidden="true">
    <div class="perf-bar__fill" style="width: 100%"></div>
  </div>
</div>
```

```css
.perf-bar { display: flex; flex-direction: column; gap: 6px; }

.perf-bar__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.perf-bar__label {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text-muted);
}

.perf-bar__pct {
  font-family: var(--font-display);
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--color-text-primary);
}

.perf-bar__track {
  height: 6px;
  background: var(--color-border-light);
  border-radius: var(--radius-pill);
  overflow: hidden;
}

.perf-bar__fill {
  height: 100%;
  background: linear-gradient(90deg, var(--unit-accent), var(--unit-accent2));
  border-radius: var(--radius-pill);
  transition: width 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}
```

---

## [RECOMMENDED] Lesson Navigation Footer

**Purpose:** Fixed bottom bar on lesson pages. Three actions. [S2]

```html
<footer class="lesson-nav" role="navigation" aria-label="Lesson navigation">
  <button class="lesson-nav__prev btn-outline" aria-label="Go to previous lesson">
    ← Previous Lesson
  </button>
  <button class="lesson-nav__save btn-ghost" aria-label="Save lesson for later">
    Save for Later
  </button>
  <button class="lesson-nav__complete btn-primary" aria-label="Mark this lesson as complete">
    Mark Lesson as Complete ✓
  </button>
</footer>
```

```css
.lesson-nav {
  position: sticky;
  bottom: 0;
  background: var(--color-bg-white);
  border-top: 1px solid var(--color-border-light);
  padding: var(--space-4) var(--space-6);
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--space-4);
  z-index: 50;
}

@media (max-width: 600px) {
  .lesson-nav {
    flex-wrap: wrap;
  }
  .lesson-nav__save { display: none; } /* optional: hide on small screens */
}
```

---

## [OPTIONAL] Quiz Question Card

**Purpose:** Single-question display with multiple choice options. [S3]

```html
<section class="quiz-question-card" aria-labelledby="question-text">
  <div class="eyebrow eyebrow--pill">Module Assessment</div>
  <h2 id="question-text" class="quiz-question-card__question">
    How does excessive screen time specifically impact neural plasticity in children under five?
  </h2>
  <ul class="quiz-options" role="radiogroup" aria-labelledby="question-text">
    <li>
      <button class="quiz-option" role="radio" aria-checked="false"
              data-correct="false">
        <span class="quiz-option__radio" aria-hidden="true"></span>
        <span>It accelerates the pruning of synaptic connections in the prefrontal cortex prematurely.</span>
      </button>
    </li>
    <li>
      <button class="quiz-option quiz-option--selected" role="radio" aria-checked="true"
              data-correct="true">
        <span class="quiz-option__radio quiz-option__radio--filled" aria-hidden="true"></span>
        <span>It may reduce the growth of white matter responsible for language, imagery, and executive literacy skills.</span>
        <span class="quiz-option__check" aria-hidden="true">✓</span>
      </button>
    </li>
  </ul>
</section>
```

```css
.quiz-question-card {
  background: var(--color-bg-white);
  border-radius: var(--radius-xl);
  padding: var(--space-8);
  box-shadow: var(--shadow-card);
  display: flex;
  flex-direction: column;
  gap: var(--space-6);
}

.quiz-question-card__question {
  font-family: var(--font-display);
  font-size: 1.15rem;
  font-weight: 700;
  line-height: 1.45;
  color: var(--color-text-primary);
}

.quiz-options {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.quiz-option {
  width: 100%;
  display: flex;
  align-items: center;
  gap: var(--space-4);
  padding: var(--space-4) var(--space-5);
  background: transparent;
  border: 1.5px solid var(--color-border-light);
  border-radius: var(--radius-md);
  text-align: left;
  cursor: pointer;
  font-size: 0.95rem;
  color: var(--color-text-primary);
  line-height: 1.5;
  transition: border-color var(--transition-fast), background var(--transition-fast);
}

.quiz-option:hover:not(:disabled) {
  border-color: var(--unit-accent);
  background: rgba(var(--unit-accent-rgb), 0.04);
}

.quiz-option--selected {
  border-color: var(--unit-accent);
  border-width: 2px;
  background: rgba(var(--unit-accent-rgb), 0.06);
}

.quiz-option--correct {
  border-color: var(--color-correct);
  background: var(--color-correct-bg);
}

.quiz-option--incorrect {
  border-color: var(--color-incorrect);
  background: var(--color-incorrect-bg);
}

.quiz-option__radio {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 2px solid var(--color-border-light);
  flex-shrink: 0;
  transition: border-color var(--transition-fast), background var(--transition-fast);
}

.quiz-option--selected .quiz-option__radio {
  background: var(--unit-accent);
  border-color: var(--unit-accent);
}

.quiz-option__check {
  margin-left: auto;
  color: var(--unit-accent);
  font-weight: 700;
}
```

---

## [OPTIONAL] Circular Progress Ring (Quiz Results)

**Purpose:** SVG circle showing mastery score percentage. [S4]

```html
<div class="progress-ring-wrap" role="img" aria-label="Mastery score: 85%">
  <svg class="progress-ring" width="200" height="200" viewBox="0 0 200 200" aria-hidden="true">
    <circle class="progress-ring__track" cx="100" cy="100" r="80"
            fill="none" stroke="#E5E7EB" stroke-width="14"/>
    <circle class="progress-ring__fill" cx="100" cy="100" r="80"
            fill="none" stroke="url(#ring-gradient)" stroke-width="14"
            stroke-linecap="round" stroke-dasharray="502.65"
            stroke-dashoffset="75.4"
            transform="rotate(-90 100 100)"/>
    <defs>
      <linearGradient id="ring-gradient" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%"   stop-color="#00F5FF"/>
        <stop offset="100%" stop-color="#CCFF00"/>
      </linearGradient>
    </defs>
  </svg>
  <div class="progress-ring__inner">
    <span class="progress-ring__score">85<span class="progress-ring__unit">%</span></span>
    <span class="progress-ring__label">Mastery Score</span>
  </div>
</div>
```

```css
.progress-ring-wrap {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.progress-ring__inner {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
}

.progress-ring__score {
  font-family: var(--font-display);
  font-size: 3.5rem;
  font-weight: 800;
  line-height: 1;
  color: var(--color-text-primary);
}

.progress-ring__unit { font-size: 1.8rem; }

.progress-ring__label {
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text-muted);
}

/* JS: set stroke-dashoffset = circumference × (1 - score/100) */
/* circumference of r=80: 2π×80 ≈ 502.65 */
/* For 85%: offset = 502.65 × 0.15 = 75.4 */
```

---

## [OPTIONAL] Course Sidebar Navigation

**Purpose:** Collapsible unit/lesson tree with progress state. [S3 right sidebar]

```html
<aside class="course-sidebar" aria-label="Course progress">
  <div class="course-sidebar__header">
    <span class="eyebrow">Course Progress</span>
    <span class="course-sidebar__score">85%</span>
  </div>
  <div class="course-sidebar__stat">
    <span>🏆</span> Current Score <strong>85%</strong>
  </div>
  <div class="course-sidebar__stat">
    <span>⏱</span> Time Elapsed <strong>04:12</strong>
  </div>
  <blockquote class="course-sidebar__quote">
    "Neural plasticity is the brain's ability to reorganize itself by forming new neural connections throughout life."
  </blockquote>
  <!-- Study material card, hint button, etc. -->
</aside>
```

```css
.course-sidebar {
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-xl);
  padding: var(--space-6);
  display: flex;
  flex-direction: column;
  gap: var(--space-5);
  min-width: 260px;
}

.course-sidebar__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.course-sidebar__score {
  font-family: var(--font-display);
  font-size: 1.6rem;
  font-weight: 800;
  color: var(--unit-accent);
}

.course-sidebar__stat {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  padding: var(--space-3) 0;
  border-bottom: 1px solid var(--color-border-light);
}

.course-sidebar__quote {
  font-style: italic;
  font-size: 0.82rem;
  color: var(--color-text-secondary);
  line-height: 1.65;
  border-left: none;
  padding: 0;
  margin: 0;
}
```

---

## [OPTIONAL] Interactive Checklist Item

```html
<li class="checklist-item">
  <button class="checkbox-box" role="checkbox" aria-checked="false"
          aria-label="Mark: Notice the serve — complete"
          onclick="this.setAttribute('aria-checked',
                   this.getAttribute('aria-checked')==='true' ? 'false' : 'true');
                   this.classList.toggle('checked');">
    <span class="checkbox-box__check" aria-hidden="true">✓</span>
  </button>
  <div class="checklist-item__content">
    <span class="checklist-item__title">1. Notice the serve</span>
    <p class="checklist-item__desc">Share the child's focus of attention. Is the child looking at something, making a sound, or moving their arms and legs?</p>
  </div>
</li>
```

---

## [OPTIONAL] Activity Card (Activity Guide)

**Purpose:** Activity with focus-type label and icon badge. [S7]

```html
<div class="activity-card">
  <div class="activity-card__header">
    <div class="icon-badge" aria-hidden="true">👁</div>
    <span class="activity-card__focus eyebrow">Focus: Sight</span>
  </div>
  <h3 class="activity-card__title">Eye Contact Moments</h3>
  <p class="activity-card__desc">Practice sustained, warm eye contact during feeding or story time.</p>
</div>
```

```css
.activity-card {
  padding: var(--space-6);
  background: var(--color-bg-white);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-lg);
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

.activity-card__header {
  display: flex;
  align-items: center;
  gap: var(--space-3);
}

.activity-card__focus {
  font-size: 0.68rem;
  color: var(--unit-accent);
}
```

---

## [OPTIONAL] Key Takeaway Grid (Worksheet)

```html
<div class="takeaway-grid" role="list">
  <div class="takeaway-item" role="listitem">
    <div class="checkbox-box" aria-hidden="true"></div>
    <div>
      <strong>Synaptic Strengthening</strong>
      <p>"Neurons that fire together, wire together." Repeated actions create permanent pathways.</p>
    </div>
  </div>
</div>
```

```css
.takeaway-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-5);
  margin: var(--space-6) 0;
}

.takeaway-item {
  display: flex;
  gap: var(--space-3);
  align-items: flex-start;
  font-size: 0.875rem;
  color: var(--color-text-secondary);
  line-height: 1.6;
}

.takeaway-item strong {
  display: block;
  color: var(--color-text-primary);
  font-weight: 600;
  margin-bottom: 2px;
}

@media (max-width: 600px) {
  .takeaway-grid { grid-template-columns: 1fr; }
}
```

---

## [OPTIONAL] Sketch / Exercise Area (Worksheet)

```html
<div class="sketch-area" role="region" aria-label="Interaction Map: sketch area">
  <div class="sketch-area__label sketch-area__label--tl eyebrow">Morning Routine</div>
  <div class="sketch-area__label sketch-area__label--br eyebrow">Bedtime Rituals</div>
  <div class="sketch-area__canvas" aria-hidden="true">
    <!-- empty drawing zone or textarea -->
  </div>
  <div class="sketch-area__columns" aria-hidden="true">
    <span>Input / Trigger</span>
    <span>Parental Return</span>
    <span>Neural Outcome</span>
  </div>
</div>
```

```css
.sketch-area {
  position: relative;
  border: 1.5px dashed var(--color-border-light);
  border-radius: var(--radius-lg);
  min-height: 320px;
  margin: var(--space-6) 0;
  overflow: hidden;
}

.sketch-area__canvas {
  width: 100%;
  height: 100%;
  min-height: 320px;
}

.sketch-area__label {
  position: absolute;
  font-size: 0.68rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--color-coral);
}

.sketch-area__label--tl { top: var(--space-4); left: var(--space-4); }
.sketch-area__label--br { bottom: var(--space-4); right: var(--space-4); }

.sketch-area__columns {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  padding: var(--space-3) var(--space-4);
  border-top: 1px solid var(--color-border-light);
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text-muted);
}
```

---

# PART 3: PAGE TEMPLATES

---

## Template 1: Unit Intro Page [S1]

**Purpose:** Entry point for each unit. Sets context, surfaces key stats, previews learning objectives, and drives to the first lesson.

**Layout:** Single centered column with a 2-column breakout section (timeline sidebar + main content).

**Page skeleton:**
1. `[CORE]` Course Nav (Variant A)
2. `[CORE]` Lesson Progress Strip
3. Unit badge + H1 title (2-tone: black first line, accent color second)
4. Lead subtitle paragraph
5. `[CORE]` Stat Card Row (3–4 cards + optional Critical Alert card)
6. `[CORE]` Section container — 2-column layout:
   - Left col: Timeline sidebar (Brain Development stages)
   - Right col: Body text + pull quote + content cards grid
7. Quiz CTA strip ("Ready for the Unit Quiz?" + Start Assessment button)
8. `[CORE]` Footer

**Design tokens specific to this template:**
- Dark hero is NOT used on this page — it's a light-on-white editorial layout
- Title uses `var(--unit-accent)` on the second line of the heading
- Stat cards use `border-left: 4px solid var(--unit-accent)`

**Print:** Not a print target — skip print styles.

**Content requirements:**
- Unit number, title (2 lines), subtitle
- 3–4 stat data points (value, label, source)
- 2–4 body paragraphs
- 1 expert pull quote + attribution
- 2–4 content cards (image + title + description)
- Quiz CTA text

---

## Template 2: Lesson Page [S2]

**Purpose:** Core content delivery. One concept per lesson, action-oriented sidebar, step-by-step breakdown, expert quote.

**Layout:** 2-column (main ~65%, sidebar ~32%) with full-width sections above/below.

**Page skeleton:**
1. `[CORE]` Course Nav (Variant A) — includes unit name
2. `[CORE]` Lesson Progress Strip
3. `[RECOMMENDED]` Hero image with KEY CONCEPT overlay — full-width image, text overlaid on bottom-left
4. Body text (lead paragraph)
5. `[RECOMMENDED]` "How it Works" section — H2 with coral left-border accent, 2×2 card grid
6. `[CORE]` Pull Quote (light variant)
7. `[RECOMMENDED]` Lesson Navigation Footer (Previous / Save / Mark Complete)

**Sidebar (sticky, position: sticky, top: 76px):**
- `[RECOMMENDED]` Try This Today card
- `[RECOMMENDED]` Need Help? card

**HTML structure:**
```html
<div class="lesson-layout">
  <main class="lesson-layout__main">
    <!-- hero image, body, how it works, pull quote -->
  </main>
  <aside class="lesson-layout__sidebar">
    <!-- try today card, need help card -->
  </aside>
</div>
```

```css
.lesson-layout {
  max-width: 1100px;
  margin: 0 auto;
  padding: var(--space-8) var(--space-6);
  display: grid;
  grid-template-columns: 1fr 320px;
  gap: var(--space-8);
  align-items: start;
}

.lesson-layout__sidebar {
  position: sticky;
  top: 80px;
  display: flex;
  flex-direction: column;
  gap: var(--space-5);
}

@media (max-width: 860px) {
  .lesson-layout {
    grid-template-columns: 1fr;
  }
  .lesson-layout__sidebar {
    position: static;
    order: -1; /* sidebar before body on mobile */
  }
}
```

**Print:** Not a primary print target, but hide sidebar and footer nav in print.

**Content requirements:**
- Lesson title, unit label, lesson number
- Key concept label + hero image (illustration preferred)
- 1–2 body paragraphs
- "How it Works" steps (3–5 numbered cards with icons)
- Expert pull quote + attribution
- 3–5 "Try This Today" action items + optional download link
- Previous lesson URL + next lesson URL

---

## Template 3: Quiz View [S3]

**Purpose:** Assessment experience. One question at a time, live score tracking in sidebar.

**Layout:** Centered content area (~720px) with sticky right sidebar (~280px).

**Page skeleton:**
1. `[CORE]` Course Nav (Variant B — quiz minimal: brand + "Exit Quiz" + avatar)
2. Header row: MODULE ASSESSMENT eyebrow pill + "Question N of N" + CURRENT MASTERY %
3. `[CORE]` Quiz progress bar (horizontal, full width of container)
4. `[OPTIONAL]` Quiz Question Card (question + options)
5. Footer row: "← Previous Question" left + "Confirm Answer →" CTA right

**Sidebar:**
- COURSE PROGRESS heading
- Current Score stat
- Time Elapsed stat
- Italic context quote
- Study material reference card (dark bg)
- "GET A HINT" button (acid yellow fill, dark text)

**Interaction flow — see Part 4.1**

**Print:** None.

**Content requirements:** Per question: question text, 4 answer options, correct answer index, explanation text (shown after answer), per-topic tag.

---

## Template 4: Quiz Results [S4]

**Purpose:** Celebrates completion, shows mastery breakdown, drives to next unit.

**Layout:** Centered single column, max-width 680px. Clean, airy.

**Page skeleton:**
1. Minimal nav (brand logo + close ✕ button)
2. `[OPTIONAL]` Circular progress ring + score + QUIZ PASSED badge
3. Personalized heading ("Incredible work, [Name].") + subtext
4. `[CORE]` Stat cards row — 3 cards: Correct, Incorrect, Total Time
5. Performance Breakdown card — unit title + `[RECOMMENDED]` topic perf bars
6. Dual CTAs: `btn-dark` (Continue to Unit N) + `btn-outline` (Review Unit N)
7. Minimal footer

**Print:** None.

**Content requirements:** Score data, per-topic scores, learner name (or fallback "there"), next unit title.

---

## Template 5: Interactive Checklist [S5]

**Purpose:** Viewable + printable reference with interactive checkboxes. Printable to a single sheet.

**Layout:** Centered single column, max-width 860px. White background.

**Page skeleton:**
1. `[CORE]` Course Nav (Variant C — brand + download/print icons)
2. Header block: left red accent border + INTERACTIVE RESOURCE eyebrow + H1 + unit subtitle + `[RECOMMENDED]` Instructor Badge
3. Section header band: gradient bg (coral → orange) + checkbox icon + section title
4. `[OPTIONAL]` Interactive checklist items (numbered, with checkbox circles)
5. Bottom row — 2 columns: `[RECOMMENDED]` Pro-Tip card + `[RECOMMENDED]` Next Milestone card
6. `[CORE]` Footer

**Print styles:**
```css
@media print {
  .course-nav,
  .milestone-card,
  .pro-tip-card { display: none; }

  body { font-size: 11pt; color: #000; background: #fff; }

  .checklist-section-header {
    background: #f0f0f0 !important;
    color: #000 !important;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }

  .checkbox-box {
    border: 2px solid #000;
    background: transparent;
  }

  .checklist-item__title { color: #000; }
  .checklist-item__desc  { color: #333; }

  @page {
    margin: 1.5cm 2cm;
    size: letter portrait;
  }
}
```

**PDF export:** `window.print()` — no library needed. Print styles handle layout.

**Content requirements:** Section title, 4–8 checklist items (number, title, description), instructor name/photo, pro-tip text, next unit info.

---

## Template 6: Worksheet [S6]

**Purpose:** Printable/PDF learning exercise with guided reflection and sketch area.

**Layout:** Narrow centered column, max-width 820px. Feels like a physical handout.

**Page skeleton:**
1. Minimal nav: brand + `btn-ghost` "Print Worksheet" + `btn-ghost` "PDF"
2. Header block: left red accent border + UNIT X: CATEGORY eyebrow + H1 + subtitle/description
3. `[OPTIONAL]` Key Takeaways section — icon badge + H2 + bordered text area + `[OPTIONAL]` takeaway grid (2-col checkboxes)
4. `[OPTIONAL]` Sketch/Exercise Area — labeled zones with dashed border
5. Footer: COURSE MATERIALS + INSTRUCTOR credit + 3-color bar decoration

**Print styles:**
```css
@media print {
  .course-nav { display: none; }

  .worksheet-header-border {
    border-left: 5px solid #FF5C3A;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }

  .sketch-area { min-height: 4in; }

  .takeaway-grid {
    grid-template-columns: 1fr 1fr;
    break-inside: avoid;
  }

  @page {
    margin: 1.5cm 2cm;
    size: letter portrait;
  }
}
```

**PDF export:** `window.print()` with print styles. Add print trigger button:
```html
<button class="btn-ghost" onclick="window.print()" aria-label="Print worksheet">
  🖨 Print Worksheet
</button>
```

**Content requirements:** Unit label, worksheet title, description, 2–4 key takeaway concepts (title + description pairs), sketch area labels (corner labels + column labels), instructor name, course name.

---

## Template 7: Activity Guide [S7]

**Purpose:** Printable reference guide with numbered framework and supporting tools sidebar.

**Layout:** 2-column (framework steps ~55%, tools sidebar ~40%) with full-width sections.

**Page skeleton:**
1. Minimal nav: brand + "Download PDF" button
2. UNIT N: CATEGORY eyebrow pill + H1 (with accent-colored keyword) + cyan underline accent + description
3. 2-column content area:
   - Left: Numbered framework steps (step cards with `[CORE]` step badges + title + description)
   - Right sidebar: Resource checklist card + `[RECOMMENDED]` Pro-Tip card + "Ready to implement?" CTA card
4. `[CORE]` Pull Quote (dark variant)
5. `[CORE]` Footer — dark bg, multi-column (brand + Course Modules + Resources + Connect)

**Age-group column layout (variant):**
```html
<div class="age-columns">
  <div class="age-column" style="--age-accent: #00F5FF;">
    <div class="age-column__header">Ages 0–2</div>
    <!-- activity cards -->
  </div>
</div>
```

```css
.age-columns {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--space-4);
}

.age-column {
  border-left: 4px solid var(--age-accent);
  padding-left: var(--space-5);
}

.age-column__header {
  font-family: var(--font-display);
  font-weight: 800;
  font-size: 0.85rem;
  color: var(--age-accent);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: var(--space-4);
}
```

**Print styles:**
```css
@media print {
  .course-nav, .course-footer { display: none; }

  .activity-guide-layout {
    display: block; /* collapse 2-col to single col */
  }

  .activity-guide-sidebar {
    display: none; /* hide sidebar in print, content is self-sufficient */
  }

  @page {
    margin: 1.5cm 2cm;
    size: letter landscape; /* landscape fits 2-column age layout better */
  }
}
```

---

# PART 4: INTERACTION PATTERNS

## 4.1 Quiz System

**Question flow (one-at-a-time):**

```javascript
const quiz = {
  questions: [],        // array of {text, options, correctIndex, topic, explanation}
  currentIndex: 0,
  answers: [],          // {questionIndex, selectedIndex, correct, topic, timeMs}
  startTime: null,
  questionStartTime: null,

  start() {
    this.currentIndex = 0;
    this.answers = [];
    this.startTime = Date.now();
    this.questionStartTime = Date.now();
    this.render();
  },

  select(optionIndex) {
    const q = this.questions[this.currentIndex];
    const correct = optionIndex === q.correctIndex;
    const timeMs = Date.now() - this.questionStartTime;

    this.answers.push({ questionIndex: this.currentIndex, selectedIndex: optionIndex, correct, topic: q.topic, timeMs });
    this.showFeedback(correct, q.explanation);
    this.updateMastery();
    // disable all other options
  },

  confirm() {
    this.currentIndex++;
    if (this.currentIndex >= this.questions.length) {
      this.showResults();
    } else {
      this.questionStartTime = Date.now();
      this.render();
    }
  },

  getMasteryScore() {
    if (!this.answers.length) return 0;
    return Math.round((this.answers.filter(a => a.correct).length / this.answers.length) * 100);
  },

  getTopicBreakdown() {
    const topics = {};
    this.answers.forEach(a => {
      if (!topics[a.topic]) topics[a.topic] = { correct: 0, total: 0 };
      topics[a.topic].total++;
      if (a.correct) topics[a.topic].correct++;
    });
    return Object.entries(topics).map(([name, data]) => ({
      name,
      pct: Math.round((data.correct / data.total) * 100)
    }));
  },

  getTotalTime() {
    const ms = Date.now() - this.startTime;
    const m = Math.floor(ms / 60000);
    const s = Math.floor((ms % 60000) / 1000);
    return `${m}:${s.toString().padStart(2,'0')}`;
  }
};
```

**Mastery level thresholds:**

| Score | Level | Label |
|-------|-------|-------|
| 90–100% | 5 | Expert |
| 75–89%  | 4 | Proficient |
| 60–74%  | 3 | Developing |
| 45–59%  | 2 | Emerging |
| 0–44%   | 1 | Foundational |

---

## 4.2 Progress & Navigation

**Lesson progress bar update:**
```javascript
function updateProgress(lessonIndex, totalLessons) {
  const pct = Math.round((lessonIndex / totalLessons) * 100);
  document.querySelector('.progress-bar-fill').style.width = pct + '%';
  document.querySelector('[data-progress-label]').textContent = pct + '% Complete';
}
```

**Mark Complete behavior:**
```javascript
function markComplete(unitId, lessonId) {
  const key = `complete_${unitId}_${lessonId}`;
  localStorage.setItem(key, 'true');
  // Update button state
  const btn = document.querySelector('.lesson-nav__complete');
  btn.textContent = '✓ Completed';
  btn.disabled = true;
  btn.setAttribute('aria-label', 'Lesson marked as complete');
  // Advance progress bar
  updateProgress(lessonId + 1, totalLessons);
}
```

---

## 4.3 Checklist Interaction

```javascript
function toggleCheckbox(btn) {
  const checked = btn.getAttribute('aria-checked') === 'true';
  btn.setAttribute('aria-checked', !checked);
  btn.classList.toggle('checked', !checked);

  // Persist state
  const key = 'checklist_' + btn.dataset.itemId;
  localStorage.setItem(key, !checked);
}

// Restore state on page load
document.querySelectorAll('.checkbox-box[data-item-id]').forEach(btn => {
  const saved = localStorage.getItem('checklist_' + btn.dataset.itemId);
  if (saved === 'true') {
    btn.setAttribute('aria-checked', 'true');
    btn.classList.add('checked');
  }
});
```

---

# PART 5: ACCESSIBILITY STANDARDS

## Minimum Requirements (Every Project)

### Semantic HTML Patterns

```html
<!-- Course page landmark structure -->
<header role="banner"><!-- nav --></header>
<main role="main" id="main-content">
  <article><!-- lesson content --></article>
  <aside aria-label="Supporting resources"><!-- sidebar --></aside>
</main>
<footer role="contentinfo"><!-- footer --></footer>

<!-- Skip link — FIRST element in body -->
<a class="skip-link" href="#main-content">Skip to main content</a>
```

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 0;
  padding: var(--space-3) var(--space-5);
  background: var(--unit-accent);
  color: var(--color-bg-dark);
  font-weight: 700;
  z-index: 9999;
}
.skip-link:focus { top: 0; }
```

### ARIA Map by Component

| Component | Required ARIA |
|-----------|--------------|
| Progress bar | `role="progressbar"` `aria-valuenow` `aria-valuemin="0"` `aria-valuemax="100"` `aria-label` |
| Quiz options | `role="radiogroup"` on list; `role="radio"` + `aria-checked` on each option |
| Checkbox | `role="checkbox"` + `aria-checked` |
| Accordion | `aria-expanded="true/false"` on trigger; `aria-controls` pointing to panel |
| Modal/overlay | `role="dialog"` + `aria-modal="true"` + `aria-labelledby` |
| Progress ring | `role="img"` + `aria-label="Mastery score: 85%"` |
| Quiz feedback | `aria-live="polite"` on feedback container |
| Score tracker | `role="status"` + `aria-live="polite"` |

### Keyboard Navigation Map

| Key | Action |
|-----|--------|
| `Tab` / `Shift+Tab` | Move focus forward/backward |
| `Enter` / `Space` | Activate buttons, toggle checkboxes |
| `Arrow Up/Down` | Navigate within radiogroup (quiz options) |
| `Escape` | Close overlay/modal, exit quiz |
| `Enter` on accordion trigger | Toggle open/closed |

### Focus Rings

```css
/* Universal — never remove, only style */
:focus-visible {
  outline: 2.5px solid var(--unit-accent, #00F5FF);
  outline-offset: 3px;
  border-radius: var(--radius-sm);
}

/* Suppress on mouse/touch interactions only */
:focus:not(:focus-visible) {
  outline: none;
}
```

### Color Contrast Requirements (WCAG AA)

| Pairing | Minimum ratio | Check |
|---------|--------------|-------|
| Body text on white | 4.5:1 | `#1A1A2E` on `#FFF` = 14.3:1 ✓ |
| Secondary text on white | 4.5:1 | `#4A4A6A` on `#FFF` = 7.1:1 ✓ |
| White text on coral CTA | 4.5:1 | Verify `#FF5C3A` at AA |
| Text on accent-colored bg | 4.5:1 | Dark text on neon accents required |
| Labels on light gray bg | 4.5:1 | `#8888A0` on `#F6F7F8` — verify |

**Rule:** Always pair neon accent colors (`#00F5FF`, `#CCFF00`, `#39FF14`) with dark text (`#0B0B12`), never white. These colors are too light for white text to meet AA.

### Screen Reader Considerations

- All images: meaningful `alt` text or `alt=""` if decorative
- Quiz score updates: wrap in `aria-live="polite"` region
- Feedback after answering: `aria-live="assertive"` (immediate, important)
- Infographics: provide `<figcaption>` or `aria-describedby` with text summary
- Animated elements: respect `prefers-reduced-motion`

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }

  .progress-bar-fill,
  .perf-bar__fill {
    transition: none;
  }
}
```

---

# PART 6: RESPONSIVE FRAMEWORK

## Breakpoint Strategy (Mobile-First)

```css
/* Base: mobile (< 480px) — single column, stacked */
/* sm: 480px+ — 2-column grids unlock */
/* md: 768px+ — 2-column lesson layout, nav links visible */
/* lg: 1024px+ — full sidebar layouts, wide containers */
/* xl: 1280px+ — max-width caps apply */

:root {
  --bp-sm:  480px;
  --bp-md:  768px;
  --bp-lg:  1024px;
  --bp-xl:  1280px;
}
```

## Per-Template Responsive Behavior

| Template | Mobile | Tablet (768px) | Desktop (1024px) |
|----------|--------|----------------|------------------|
| Unit Intro | Stat cards stack 1-col; timeline becomes vertical | 2-col stat cards; timeline 2-col | Full 2-col layout |
| Lesson Page | Sidebar above main; footer 2-col | Sidebar right, sticky | 65/35 grid |
| Quiz View | Sidebar hidden (score in header only); options full-width | Sidebar collapses to strip | 60/35 grid |
| Quiz Results | Cards stack; ring smaller | Cards 3-col | Centered 680px |
| Checklist | Single col, full-width | Same | Max-width 860px centered |
| Worksheet | Takeaway grid 1-col | 2-col | Max-width 820px centered |
| Activity Guide | Steps + sidebar stack; sidebar above | 2-col unlocks | 55/40 grid |

## Touch Targets

```css
/* Minimum 44×44px touch targets on all interactive elements */
button, a, [role="checkbox"], [role="radio"] {
  min-height: 44px;
  min-width: 44px;
}

/* Exception: inline text links don't need height override */
p a { min-height: auto; }
```

## Quiz on Mobile

```css
/* On mobile: sidebar becomes a top strip */
@media (max-width: 767px) {
  .quiz-layout {
    display: block;
  }

  .course-sidebar {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    border-radius: 0;
    border-left: none;
    border-right: none;
    padding: var(--space-3) var(--space-5);
    /* collapse to just score + time */
  }

  .course-sidebar__quote,
  .course-sidebar__study-material { display: none; }
}
```

---

# PART 7: GAP ANALYSIS

## Existing Projects vs. Target System

| Feature / Pattern | `ready_for_whats_next.html` | `raising_humans.html` | Target System | Status |
|---|---|---|---|---|
| Per-unit accent colors | ✓ (5 units, JS-applied) | ✓ (8 units, CSS classes) | ✓ CSS custom props | **Aligned** |
| Dark/light color architecture | ✓ Full dark default + light mode toggle | Light only | Both available | **Needs evolution** (raising_humans needs dark mode option) |
| CSS custom property token system | Partial (some tokens, some hardcoded) | Minimal (few vars) | Full token system | **Needs evolution** |
| Font system: Manrope + IBM Plex Sans | ✗ (Inter + Outfit + Noto) | ✓ | Manrope + IBM Plex Sans | **Needs evolution** (ready_for_whats_next needs font update) |
| One-question quiz with progress dots | ✓ | ✗ (all-at-once) | ✓ | **Aligned** (rfwn) / **Needs evolution** (raising_humans) |
| Quiz score with per-topic breakdown | ✗ | ✗ | ✓ | **Net New** |
| Circular progress ring (quiz results) | ✗ | ✗ | ✓ | **Net New** |
| Mastery level badges | ✗ | ✗ | ✓ | **Net New** |
| Timer tracking | ✗ | ✗ | ✓ | **Net New** |
| Lesson nav footer (Prev/Save/Complete) | ✗ | ✗ | ✓ | **Net New** |
| Lesson progress strip (unit/lesson N of N) | ✗ | ✗ | ✓ | **Net New** |
| "Try This Today" sidebar card | ✗ | ✗ | ✓ | **Net New** |
| Instructor attribution badge | ✗ | ✗ | ✓ | **Net New** |
| Pull quote component | Partial (styling, no component) | ✓ (border-left style) | Full component with deco marks | **Needs evolution** |
| Stat card row | ✗ | ✓ (stat callout box) | Full stat card row | **Needs evolution** |
| Accordion expand/collapse | ✓ (animated) | ✓ (basic) | ✓ with ARIA | **Aligned** (rfwn) / **Needs evolution** (raising_humans needs ARIA) |
| Keyword tooltips | ✓ | ✗ | Optional | **Aligned** (rfwn) |
| Light/dark mode toggle | ✓ | ✗ | Optional | **Aligned** (rfwn) |
| Multilingual toggle | ✓ (4 languages) | ✗ | Optional | **Aligned** (rfwn) |
| Printable worksheet template | ✗ | ✗ | ✓ | **Net New** |
| Interactive checklist template | ✗ | ✗ | ✓ | **Net New** |
| Activity guide template | ✗ | ✗ | ✓ | **Net New** |
| Responsive layout (sidebar collapse) | ✓ | ✓ | ✓ | **Aligned** |
| Keyboard navigation / focus rings | ✓ (custom rings) | ✗ | Required | **Aligned** (rfwn) / **Net New** (raising_humans) |
| ARIA on interactive elements | Partial | Minimal | Full | **Needs evolution** |
| localStorage progress persistence | Partial | ✗ | Recommended | **Needs evolution** |
| Skip link | ✗ | ✗ | Required | **Net New** (both) |
| @prefers-reduced-motion | ✗ | ✗ | Required | **Net New** (both) |
| Print stylesheet | ✗ | ✗ | Required for 3 templates | **Net New** |
| Infographic components | ✗ | ✓ (timeline, funnel, table, chart) | Optional | **Aligned** (raising_humans) |

---

# PART 8: NEW PROJECT QUICKSTART CHECKLIST

Use this when starting any new course, module, or interactive resource. Fill in all fields before writing a line of code.

---

**Project Basics**

- [ ] **Project name:** _______________
- [ ] **Target audience:** _______________ (age range, role, context)
- [ ] **Tone / voice:** _______________ (e.g., "warm and research-backed" / "encouraging and practical")
- [ ] **Number of units:** ___  **Lessons per unit:** ___
- [ ] **Downloadable resources needed:** ☐ Checklist ☐ Worksheet ☐ Activity Guide ☐ Other: ___

---

**Typography Slots**

- [ ] **Display font (serif/display slot):** _______________ (default: Manrope)
- [ ] **Body font (sans-serif slot):** _______________ (default: IBM Plex Sans)
- [ ] Add Google Fonts `<link>` with both families

---

**Color Architecture**

- [ ] **Dark background:** _______________ (default: `#0B0B12`)
- [ ] **Light background:** _______________ (default: `#F6F7F8`)
- [ ] **White content areas:** `#FFFFFF`
- [ ] **Primary action color (coral slot):** _______________ (default: `#FF5C3A`)
- [ ] **Per-unit accent pairs:** (fill one row per unit)

| Unit | Accent 1 | Accent 2 |
|------|----------|----------|
| 1    |          |          |
| 2    |          |          |
| ...  |          |          |

---

**Page Templates Needed**

- [ ] Unit Intro Page
- [ ] Lesson Page
- [ ] Quiz View
- [ ] Quiz Results
- [ ] Interactive Checklist
- [ ] Worksheet
- [ ] Activity Guide

---

**Quiz Format**

- [ ] Per-lesson quizzes (short, 3–5 questions)
- [ ] Per-unit quizzes (longer, 8–15 questions)
- [ ] Both
- [ ] **Per-topic tags** defined? (needed for topic performance breakdown)

---

**Instructor Attribution**

- [ ] Instructor name: _______________
- [ ] Instructor title: _______________
- [ ] Instructor avatar image: _______________

---

**Optional Features**

- [ ] Light/dark mode toggle
- [ ] Multilingual toggle — languages: _______________
- [ ] Mastery level badges (5-level system)
- [ ] Live session indicator
- [ ] Timer tracking in quiz
- [ ] localStorage progress persistence
- [ ] Keyword tooltip definitions

---

**Accessibility Checklist (Before Launch)**

- [ ] Skip link added as first body element
- [ ] All images have `alt` text (or `alt=""` if decorative)
- [ ] All interactive elements are keyboard-navigable
- [ ] Quiz uses `role="radiogroup"` + `role="radio"` + `aria-checked`
- [ ] Accordions use `aria-expanded`
- [ ] Score/feedback uses `aria-live`
- [ ] Focus rings visible (never `outline: none` without alternative)
- [ ] Color contrast verified (WCAG AA) for all text/bg combinations
- [ ] `@prefers-reduced-motion` rules in place
- [ ] Tested with screen reader (VoiceOver or NVDA)

---

**Pre-Launch Review**

- [ ] Preview at localhost:8000 on desktop
- [ ] Preview on mobile (or browser devtools mobile emulation)
- [ ] Test print output for any printable templates (File → Print → Preview)
- [ ] All quiz questions answered; results page renders correctly
- [ ] All accordion items expand and collapse
- [ ] All external links and download links tested
- [ ] Confirm with Ange before pushing to GitHub Pages

---

*End of Course Design System Specification v1.0*
*Maintained by: Claude Code · Owned by: Angela Valenti*
