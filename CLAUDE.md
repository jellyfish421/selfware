# Selfware — Site Structure & Color Guide

Single-file site. Everything lives in `index.html` — all CSS is in the `<style>` block at the top, all HTML below `</style>`.

## Color system

All colors are CSS custom properties defined in `:root` (around line 11). Change a variable there and it updates everywhere on the page.

```css
:root {
    --bg: #080808;          /* darkest background (hero, nav, AI section) */
    --bg-2: #111111;        /* slightly lighter surface */
    --bg-3: #1c1c1c;        /* card/input backgrounds */
    --bg-4: #242424;        /* rarely used extra layer */
    --text: #ffffff;        /* primary text */
    --muted: #606060;       /* very muted text / labels */
    --muted-2: #999999;     /* secondary body text */
    --accent: #ffffff;      /* used for active indicators / borders */
    --accent-light: #cccccc;/* subtle tints */
    --accent-dim: rgba(255,255,255,0.06);  /* icon bg, tag bg */
    --border: rgba(255,255,255,0.08);      /* default dividers */
    --border-2: rgba(255,255,255,0.14);    /* slightly stronger border */
    --border-accent: rgba(255,255,255,0.16); /* highlighted borders */
    --green: #22c55e;       /* positive indicators */
    --red: #ef4444;         /* negative indicators */
    --yellow: #f59e0b;      /* warning/watch indicators */
}
```

### Current accent color: orange `#f97316`

The brand accent is **orange (`#f97316`)**, hardcoded directly on the elements below (not via `--accent`). To change the accent color, do a find-and-replace of `#f97316` across the file. Also replace `rgba(249,115,22,` with the new color's rgba equivalent for the tinted backgrounds.

Orange is currently applied to:
- `.banner { background }` — top announcement bar
- `.logo span` — the "ware" in the nav logo
- `.btn-accent { background }` — all CTA buttons
- `.label` — section eyebrow labels (THE PROBLEM, THE SOLUTION, etc.)
- `.ai-hero-label` — the "The Centerpiece" pill in AI section
- `.ai-pulse` — pulsing dot animation
- `.mockup-ai-dot` and `.mockup-ai-title` — AI card in the hero mockup
- `.mockup-nav-item.active { border-left }` — active nav item in mockup
- `.feature-icon { background }` — icon backgrounds in features grid (as rgba tint)
- `.pricing-card.featured { border-color }` — featured pricing card border
- `pricing-list li::before` — checkmarks in pricing lists
- Footer logo `span` — the "ware" in the footer logo
- RevOps "Your Selfware AI advisor" header (inline HTML, ~line 1519)

### To change the overall darkness
Change `--bg`, `--bg-2`, `--bg-3`. These cascade everywhere. Lighter values = less contrasty dark mode.

---

## Light sections (white-background sections)

Three sections get a white background via `class="light-section"`:
- `#problem` — The Problem
- `#features` — Features grid
- `#pricing` — Pricing cards

The `.light-section` class (defined right after `:root`) redefines all the same custom properties to light-mode values. Every `var()` inside those sections auto-flips — no per-element overrides needed.

```css
.light-section {
    --bg: #fafafa;
    --bg-2: #f4f4f4;
    --text: #080808;
    --accent: #080808;
    --muted-2: #555555;
    /* ... etc */
    background: #ffffff;
    color: #080808;
}
```

To make a section light: add `class="light-section"` to the `<section>` tag.
To make a section dark: remove `class="light-section"` (dark is the default).

### Caveats inside light sections
Some elements have hardcoded dark backgrounds that sit inside a light section (the dark featured pricing card, the philosophy callout box). These need manual overrides if you change colors — see the block of `.light-section .pricing-card.featured ...` and `.light-section .philosophy-box .sub` rules in the CSS.

---

## Hardcoded values (not controlled by variables)

| Location | Value | Why hardcoded |
|---|---|---|
| `.banner { background }` | `#f97316` | Orange brand color |
| `.btn-accent { background }` | `#f97316` | Orange CTA button |
| `.btn-accent { color }` | `white` | White text on orange button |
| `.logo span { color }` | `#f97316` | Orange "ware" in nav logo |
| `.label { color }` | `#f97316` | Orange section eyebrow labels |
| `.ai-hero-label` | `#f97316` | Orange AI section pill |
| `.ai-pulse` | `#f97316` | Orange pulse dot |
| `.mockup-nav-item.active { border-left }` | `#f97316` | Orange active nav indicator |
| `.feature-icon { background }` | `rgba(249,115,22,0.1)` | Orange-tinted icon bg |
| `.pricing-card.featured { border-color }` | `rgba(249,115,22,0.35)` | Orange featured card border |
| `.mockup-ai-dot / .mockup-ai-title` | `#f97316` | Orange AI card accent in mockup |
| `.philosophy-box { background }` | `linear-gradient(#111111, #0d0d0d)` | Dark callout box |
| `.mockup-ai-card { background }` | `linear-gradient(#111111, #0d0d0d)` | Dark AI card in mockup |
| `.ai-demo { background }` | `linear-gradient(#111111, #0b0b0b)` | AI demo box |
| `.pricing-card.featured { background }` | `linear-gradient(#111111, #0d0d0d)` | Dark featured pricing card |
| RevOps compare card (inline HTML, ~line 1519) | `linear-gradient(#111111, #0d0d0d)` | Dark "Selfware" compare card |
| Founder name (inline HTML) | `color:white` | Sits in a dark section |
| Footer logo span | `color:#f97316` | Orange "ware" in footer logo |

---

## Page sections (in order)

```
Banner          — .banner                       orange background, always visible
Nav             — nav                           sticky, dark, logo = "self" white + "ware" orange
Hero            — #hero-wrap                    dark, CSS dashboard mockup in background
                  — credibility line below CTA: "Built for lead gen agencies by a lead gen agency..."
Problem         — #problem.light-section        WHITE background
AI Advisor      — #ai-advisor                   dark
RevOps          — (no id)                       dark
Solution        — #solution                     dark
Features        — #features.light-section       WHITE background
Founder         — #story                        dark
Pricing         — #pricing.light-section        WHITE background
Final CTA       — #apply                        dark
Footer          — footer                        dark, logo = "self" white + "ware" orange
```

---

## Logo files

`logo-generator.html` — open in a browser to download PNG exports of the logo. Currently generates:
- Wordmark (640×120): transparent bg + black bg
- Profile picture (500×500): transparent bg + black bg, logo centered

`logo.svg` — transparent background SVG wordmark
`logo-black-bg.svg` — black background SVG wordmark

---

## Booking link

All "Book a Demo" buttons point to `https://cal.com/jellyfishnocode/selfware`. Search for that URL to find and update all instances.

## Deployment

Push to `master` branch on `jellyfish421/selfware`. GitHub Pages serves it at `selfwaredev.com`.
HTTPS certificate: Let's Encrypt via GitHub Pages. If DNS check is stuck, remove and re-add the custom domain in repo Settings → Pages to force a fresh check.
