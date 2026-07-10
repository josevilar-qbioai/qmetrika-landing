# QMetrika Labs — Design System

Reference document for the visual identity of **qmetrika.xyz**.
Use this when creating new pages, blog posts, or updating existing content.

Last updated: July 2026

---

## 0. Brand identity

### Logo files

All brand assets are in `assets/`:

| File | Description | Use |
|------|-------------|-----|
| `simbolo-q.svg` | Q symbol only (light bg) | Favicon, social, small contexts |
| `simbolo-q-negativo.svg` | Q symbol only (dark bg) | Dark sections, overlays |
| `logo-qmetrika.svg` | Symbol + "qmetrika" wordmark (light bg) | Headers, documents |
| `logo-qmetrika-negativo.svg` | Symbol + wordmark (dark bg) | Dark backgrounds |
| `favicon.svg` | SVG favicon (same as symbol) | All pages `<link rel="icon">` |

### The Q symbol

The symbol is a geometric Q built from concentric circles:

```svg
<circle cx="28" cy="28" r="18" fill="none" stroke="#1B1B18" stroke-width="4.5"/>  <!-- outer ring -->
<circle cx="41" cy="41" r="9.6" fill="#E9E7E0"/>  <!-- background mask -->
<circle cx="41" cy="41" r="7.4" fill="#1B1B18"/>   <!-- ink ring of dot -->
<circle cx="41" cy="41" r="5.4" fill="#A6542E"/>   <!-- accent core of dot -->
```

The dot sits at the bottom-right of the Q, offset from center. Three colors: ink stroke, background mask, accent core. ViewBox: `6 6 46 46`.

For dark backgrounds, swap ink ↔ background but keep accent:
- Outer ring stroke: `#E9E7E0` (was `#1B1B18`)
- Background mask: `#1B1B18` (was `#E9E7E0`)
- Ink ring: `#E9E7E0` (was `#1B1B18`)
- Accent core: `#A6542E` (unchanged)

### Brand mark in navigation

The Q symbol replaces the old text-based square. It's rendered as inline SVG at 26×26px:

```html
<svg class="brand-mark" width="26" height="26" viewBox="6 6 46 46" fill="none"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="28" cy="28" r="18" stroke="#1B1B18" stroke-width="4.5"/>
  <circle cx="41" cy="41" r="9.6" fill="#E9E7E0"/>
  <circle cx="41" cy="41" r="7.4" fill="#1B1B18"/>
  <circle cx="41" cy="41" r="5.4" fill="#A6542E"/>
</svg>
```

CSS: `.brand-mark { width: 26px; height: 26px; flex-shrink: 0; }`

Blog posts use class `.logo-mark` instead of `.brand-mark` (same SVG, different class name).

### Favicon

All pages include the SVG favicon. Root-level pages:
```html
<link rel="icon" type="image/svg+xml" href="assets/favicon.svg">
```

Blog posts (one level deep):
```html
<link rel="icon" type="image/svg+xml" href="../assets/favicon.svg">
```

---

## 1. Foundations

### Color palette

```css
:root {
  /* Surface */
  --bg:       #E9E7E0;   /* page background — warm off-white */
  --panel:    #DEDBD1;   /* card/callout background — one step darker */
  --input:    #F1EFE8;   /* form input background */

  /* Text */
  --ink:      #1B1B18;   /* primary text — near-black warm */
  --muted:    #57544B;   /* secondary text — body copy, descriptions */
  --faint:    #7A776C;   /* tertiary text — labels, metadata */

  /* Lines & borders */
  --rule:     #CFCCC2;   /* 1px borders, grid gaps, dividers */

  /* Accent */
  --accent:   #A6542E;   /* terracotta — kickers, highlights, links */
  --accent-lt:#D98A5E;   /* lighter accent — dark-bg contexts */

  /* Dark surface (inverted blocks) */
  --dark:     #1B1B18;   /* dark section background */
  --dark-fg:  #E9E7E0;   /* text on dark background */
  --dark-muted:#B4B0A5;  /* secondary text on dark background */
}
```

All elements use **no border-radius** (sharp corners everywhere — brand signature).

### Typography

| Role | Family | Weight | Size | Notes |
|------|--------|--------|------|-------|
| Headings | Space Grotesk | 500 | clamp values | letter-spacing: -.025em to -.035em |
| Body | Space Grotesk | 400 | 15.5–16px | line-height: 1.65–1.85 |
| UI / Labels | IBM Plex Mono | 400–600 | 10–13.5px | letter-spacing: .06–.14em, uppercase for labels |
| Code / Mono | IBM Plex Mono | 400 | 12–13px | used in nav, stats, kickers, callouts |

Google Fonts import (always include both):
```html
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```

### Selection highlight

```css
::selection { background: var(--accent); color: var(--bg); }
```

---

## 2. Page types and layout widths

| Page type | Container class | max-width | Padding | Example files |
|-----------|----------------|-----------|---------|---------------|
| **Landing** | `.shell` | 1180px | 0 (sections use 48px) | `index.html`, `en.html` |
| **Thesis / Long-form** | `.shell` | 960px | 0 48px | `TOKEN_CAPITAL_QMETRIKA_ES.html` |
| **Blog post** | `.wrap` | 740px | 0 32px | `blog/energyfingerprint.html` |
| **Blog index** | `.wrap` | 860px | 0 40px | `blog/index.html` |

Landing pages have section padding at `88px 48px`. Blog posts use `52px 0` for the body. Thesis docs use `88px 0` for sections.

---

## 3. Navigation

The nav bar is consistent across all pages:

```css
nav {
  position: sticky; top: 0; z-index: 50–100;
  border-bottom: 1px solid var(--rule);
  background: rgba(233,231,224,.9);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
```

### Brand mark

A 24×24px square with `--ink` background and `--bg` text. IBM Plex Mono 600 13px. Contains the letter "Q".

```html
<div class="brand-mark">Q</div>
<span class="brand-name">QMetrika Labs</span>
```

### Nav links

IBM Plex Mono 11.5px, color `--muted`, hover `--ink`. Active links use `--accent`.

**Bracket notation** is the brand convention:
```
[ filosofía ]  [ bio-ia ]  [ blog ]  [ contacto ]
```

### Language switcher

On landing pages: inline text `es/en` with accent-colored slash.
On blog posts: bordered pill `.lang-switch` with border and padding.
On thesis pages: inline link in nav similar to landing.

**Convention:** Spanish pages are the originals. English mirrors add `-en.html` suffix for blog posts, or use `en.html` / `TOKEN_CAPITAL_QMETRIKA.html` (no suffix) for standalone pages.

### Responsive (≤860px)

Nav links are hidden; only the brand mark remains visible. Padding reduces to 22px.

---

## 4. Component library

### 4.1 Section kicker

Small monospace label above section headings. Always in accent color.

```html
<div class="kick">// notas_del_laboratorio</div>     <!-- landing / blog index -->
<div class="kicker">// 01 · tesis</div>                <!-- thesis (ES) -->
<div class="sec-kicker">// 01_thesis</div>              <!-- thesis (EN) -->
```

Format: `// section_name` (underscore style) or `// 01 · nombre` (numbered with middle dot).

**CSS:**
```css
.kick, .kicker, .sec-kicker {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  letter-spacing: .1em;
  color: var(--accent);
  margin-bottom: 14–16px;
}
```

### 4.2 Headings

```css
h1 { font-weight: 500; font-size: clamp(2.6rem, 6vw, 4.1rem); letter-spacing: -.035em; line-height: 1.03–1.08; }
h2 { font-weight: 500; font-size: clamp(1.8rem, 3.5vw, 2.4rem); letter-spacing: -.025em; }
h3 { font-weight: 600; font-size: 16–18px; }
```

Accent highlight within headings: `<span class="hl">word</span>` → `color: var(--accent)`.

### 4.3 Subtitle / lead paragraph

```css
.sub, .lede {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 13.5–15px;
  line-height: 1.7–1.75;
  color: var(--muted);
  max-width: 620px;
}
.sub b, .lede b { color: var(--ink); font-weight: 600; }
.sub em, .lede em { color: var(--accent); font-style: italic; }
```

### 4.4 Grid cards

The signature layout: cards separated by 1px gaps that reveal `--rule` color behind them.

```css
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background: var(--rule);        /* gap color */
  border: 1px solid var(--rule);  /* outer border */
}
.cards-2 { grid-template-columns: repeat(2, 1fr); }
.card {
  background: var(--bg);
  padding: 32px 28px;
}
```

Each card has a file-name label:

```html
<div class="fname">module_name</div>
```

```css
.card .fname {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10.5px;
  color: var(--accent);
  margin-bottom: 16px;
  letter-spacing: .12em;
  text-transform: uppercase;
  font-weight: 600;
}
```

Semantic color variants for fname (thesis pages):
- Default (design): `--accent` (#A6542E)
- Build: `--c-build` (#1B1B18 ink)
- Test: `--c-test` (#8B6847 warm brown)
- Learn: `--c-learn` (#5E7E65 muted green)

Card body text: IBM Plex Mono 12px, color `--faint`. Bold → `--ink`. Em → `--accent`.

### 4.5 Pillars (landing page only)

4-column grid with vertical 1px borders (no gaps, just borders between columns).

```css
.pillars {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  border-top: 1px solid var(--rule);
  border-bottom: 1px solid var(--rule);
}
.pillar { padding: 34px 26px; border-right: 1px solid var(--rule); }
.pillar:last-child { border-right: none; }
.pillar .idx { /* IBM Plex Mono 10.5px, accent */ }
```

### 4.6 Principles grid

2-column 1px-gap grid with panel background. Used on landing, blog posts, and thesis pages.

```css
.principles, .principle-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1px;
  background: var(--rule);
  border: 1px solid var(--rule);
}
.principle, .pcard {
  background: var(--panel);
  padding: 22–26px;
}
.principle .pid, .pcard .pid {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  color: var(--accent);
  font-weight: 600;
}
```

### 4.7 Stats row

Flex container with 1px gaps. Numbers large and prominent.

```css
.stats, .stat-row {
  display: flex;
  gap: 1px;
  background: var(--rule);
  border: 1px solid var(--rule);
}
.stat {
  flex: 1;
  background: var(--bg);     /* or var(--panel) inside panel sections */
  padding: 22–24px;
  font-family: 'IBM Plex Mono', monospace;
}
.stat .n, .stat .v {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 600;
  font-size: 26–30px;
  line-height: 1;
}
.stat .n.a, .stat .v { color: var(--accent); }
.stat .l {
  font-size: 10px;
  color: var(--faint);
  text-transform: uppercase;
  letter-spacing: .05em;
  margin-top: 8px;
}
```

### 4.8 Pull quote

```css
.pull, .pullquote {
  font-size: clamp(1.2rem, 2.5vw, 1.55rem);
  font-weight: 400–500;
  font-style: italic;        /* .pull only */
  color: var(--ink);
  border-left: 2–3px solid var(--accent);
  padding: 6px 0 6px 24px;
  margin: 36–40px 0;
  max-width: 58ch;
}
.pull b, .pullquote b {
  color: var(--accent);
  font-weight: 600;
}
```

### 4.9 Callout — light

Panel background with accent left border.

```css
.callout {
  background: var(--panel);
  border: 1px solid var(--rule);
  border-left: 3px solid var(--accent);
  padding: 22px 26px;
  margin: 26px 0;
}
.callout .lab {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: .14em;
  text-transform: uppercase;
  color: var(--accent);
  font-weight: 600;
}
.callout p {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 12.5px;
  color: var(--faint);
  line-height: 1.75;
}
```

### 4.10 Callout — dark

Inverted block. Used for emphasis (Agent-Board section, key insights).

```css
.callout-dark {
  background: var(--ink);
  border: 1px solid var(--ink);
  color: var(--dark-fg);
  padding: 26px 28px;
  margin: 26px 0;
}
.callout-dark .lab { color: var(--accent-lt); }
.callout-dark p { color: var(--dark-muted); }
.callout-dark p b { color: var(--dark-fg); }
.callout-dark p em { color: var(--accent-lt); }
```

### 4.11 Tables

```css
.table-scroll, .table-wrap { overflow-x: auto; border: 1px solid var(--rule); }
table { border-collapse: collapse; width: 100%; font-size: 12.5–13.5px; }
th, td { text-align: left; padding: 12px 14–16px; border-bottom: 1px solid var(--rule); }
thead th {
  background: var(--panel);
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10–11px;
  letter-spacing: .06em;
  text-transform: uppercase;
  font-weight: 600;
}
tbody td { color: var(--muted); }
tbody td b { color: var(--ink); }
/* Highlight row */
tr.highlight-row td { background: rgba(166,84,46,.08); color: var(--ink); }
tr.highlight-row td b { color: var(--accent); }
```

### 4.12 Numbered steps (thesis pages)

```css
.steps {
  counter-reset: step;
  list-style: none;
  display: grid;
  gap: 1px;
  background: var(--rule);
  border: 1px solid var(--rule);
}
.steps li {
  padding: 18px 22px 18px 62px;
  background: var(--bg);
  font-size: 14.5px;
  color: var(--muted);
}
.steps li::before {
  counter-increment: step;
  content: counter(step);
  /* 30x30 accent square, centered number */
  width: 30px; height: 30px;
  background: var(--accent);
  color: var(--dark-fg);
  font-family: 'IBM Plex Mono', monospace;
  font-weight: 600;
  font-size: 14px;
}
```

### 4.13 Diagram frames (thesis pages)

SVG diagrams are wrapped in panel-colored containers:

```css
.diagram-frame {
  background: var(--panel);
  border: 1px solid var(--rule);
  padding: 24px;
  margin: 20px 0;
}
```

Legend dots below diagrams are **square** (no border-radius):

```css
.dot { width: 10px; height: 10px; display: inline-block; }
```

### 4.14 Buttons

Two variants:

```css
/* Solid — primary action */
.btn-solid, .btn-teal {
  background: var(--ink);
  color: var(--dark-fg);
  padding: 12–14px 22–26px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 12.5–13.5px;
}
.btn-solid:hover, .btn-teal:hover {
  background: var(--accent);
}

/* Outline — secondary action */
.btn-line, .btn-ghost {
  border: 1px solid var(--ink);
  color: var(--ink);
  background: transparent;
}
.btn-line:hover, .btn-ghost:hover {
  background: var(--ink);
  color: var(--dark-fg);
}
```

### 4.15 Tags (blog)

```css
.tag {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: .06em;
  padding: 3px 10px;
  border: 1px solid var(--rule);
  color: var(--muted);
  border-radius: 0;       /* always sharp */
}
.tag.a, .tag.t, .tag.g, .tag.p {
  color: var(--accent);
  border-color: var(--accent);
}
```

### 4.16 Badges (thesis pages)

```css
.badge {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: .08em;
  text-transform: uppercase;
  padding: 4px 10px;
  font-weight: 600;
  border: 1px solid var(--rule);
}
/* Semantic colors */
.badge.design { color: var(--c-design); border-color: var(--c-design); }
.badge.build  { color: var(--c-build);  border-color: var(--c-build); }
.badge.test   { color: var(--c-test);   border-color: var(--c-test); }
```

### 4.17 Formula block (blog posts)

```css
.formula {
  border: 1px solid var(--rule);
  background: var(--panel);
  padding: 32px 28px;
  text-align: center;
}
.formula .f {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 2rem;
  color: var(--ink);
  letter-spacing: .05em;
}
.formula .f .sym { color: var(--accent); font-weight: 600; }
.formula .f .op  { color: var(--faint); margin: 0 8px; }
.formula .desc {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  color: var(--faint);
  max-width: 56ch;
  margin: 0 auto;
}
```

### 4.18 CTA box (blog posts)

```css
.cta-box {
  border: 1px solid var(--rule);
  background: var(--panel);
  padding: 28px;
  text-align: center;
}
```

### 4.19 Publications list (landing page)

```css
.pubs {
  display: flex;
  flex-direction: column;
  border: 1px solid var(--rule);
  background: var(--rule);
  gap: 1px;
}
.pub {
  background: var(--panel);
  padding: 26px 28px;
  display: grid;
  grid-template-columns: 60px 1fr;
  gap: 20px;
}
.pub .pn { /* accent-colored paper number */ }
```

### 4.20 Footer

```css
footer {
  padding: 28–32px 0–48px;
  border-top: 1px solid var(--rule);
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  color: var(--faint);
}
footer a { color: var(--accent); }
```

---

## 5. SVG diagram colors (thesis pages)

When embedding SVG diagrams, map conceptual phases to these colors:

| Phase | CSS variable | Hex | Use |
|-------|-------------|-----|-----|
| Design | `--c-design` | #A6542E | Primary accent / terracotta |
| Build | `--c-build` | #1B1B18 | Ink / dark |
| Test | `--c-test` | #8B6847 | Warm brown |
| Learn | `--c-learn` | #5E7E65 | Muted sage green |

Legend dots use these same colors as square `background` with no border-radius.

---

## 6. Blog post template

When creating a new blog post, follow this structure:

```html
<!DOCTYPE html>
<html lang="es"> <!-- or "en" -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Post Title — QMetrika Labs Blog</title>
  <meta name="description" content="...">
  <!-- Google Fonts (always both families) -->
  <style>
    :root {
      --bg:#E9E7E0; --panel:#DEDBD1; --ink:#1B1B18;
      --muted:#57544B; --faint:#7A776C; --rule:#CFCCC2;
      --accent:#A6542E; --accent-lt:#D98A5E; --dark-fg:#E9E7E0;
    }
    /* ... component styles as needed ... */
    .wrap { max-width: 740px; margin: 0 auto; padding: 0 32px; }
  </style>
</head>
<body>
  <nav>
    <div class="inner">
      <a href="../" class="logo">
        <div class="logo-mark"><span>Q</span></div>
        <span class="logo-name">QMetrika Labs</span>
      </a>
      <div class="links">
        <a href="../">Home</a>
        <a href="./">Blog</a>
        <a href="../#contacto">Contacto</a>
        <a href="post-name-en.html" class="lang-switch">EN</a>
      </div>
    </div>
  </nav>

  <div class="wrap">
    <div class="post-header">
      <a href="./" class="back">← Blog</a>
      <div class="post-date">MES 2026</div>
      <h1>Título del <em>post</em></h1>
      <p class="excerpt">Descripción breve en IBM Plex Mono.</p>
      <div class="post-tags">
        <span class="tag t">bio-ia</span>
        <span class="tag">tema</span>
      </div>
    </div>

    <div class="post-body">
      <h2>Section heading</h2>
      <p>Body text. <b>Bold</b> for emphasis, <em>accent italic</em> for terms.</p>
      <!-- Use components: .pullquote, .stat-row, .principle-grid, .formula, .table-wrap, .cta-box -->
    </div>

    <footer><p><a href="./">← blog</a> · <a href="../">qmetrika_labs</a> · 2026</p></footer>
  </div>
</body>
</html>
```

---

## 7. Anti-patterns (things to avoid)

- **No border-radius anywhere.** Every element is sharp-cornered.
- **No gradients** on UI elements (only the hero has the subtle horizontal grid-line pattern).
- **No shadows.** Depth is conveyed through 1px borders and panel/bg color difference.
- **No color outside the palette.** No blues, purples, or greens except `--c-learn` (#5E7E65) in diagrams.
- **No emoji** in page content.
- **No heavy font weights** on headings. h1/h2 use weight 500, not 700.
- **No generic fonts.** Always Space Grotesk + IBM Plex Mono. Never fall back to Arial, Helvetica, etc.

---

## 8. Anti-bot email obfuscation

Display email with `[at]` and use JavaScript to construct the mailto:

```html
<a href="#" class="email-link" data-u="user" data-d="domain.com">user[at]domain.com</a>
<script>
document.querySelectorAll('.email-link').forEach(a => {
  a.href = 'mailto:' + a.dataset.u + '@' + a.dataset.d;
});
</script>
```

---

## 9. Translation conventions

- "flywheel" → "espiral de acumulación"
- "fine-tuning" stays in English (italic)
- "el ratio" (masculine article)
- "dominio" (not "dominio profundo")
- Use impersonal constructions over first person plural
- Blog file naming: Spanish originals keep their name; English translations add `-en.html` suffix
- Brand links: Spanish pages → `href="index.html"` or `"../"`, English pages → `href="en.html"` or `"../en.html"`

---

## 10. Responsive breakpoints

| Breakpoint | Landing | Blog | Thesis |
|------------|---------|------|--------|
| ≤860px | Nav hidden, 1-col grids, 22px padding | — | — |
| ≤600px | — | 1-col principles, nav items hidden | Similar to blog |

Key responsive changes:
- Nav links collapse (only brand + language visible)
- Grid cards → single column
- Pillars → 2 columns
- Stats → flex-wrap
- Padding: 48px → 22px
