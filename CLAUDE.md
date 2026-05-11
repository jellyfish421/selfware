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
    --accent: #ffffff;      /* CTA button background + active indicators */
    --accent-light: #cccccc;/* labels, pricing plan names, logo subtext */
    --accent-dim: rgba(255,255,255,0.06);  /* icon bg, tag bg */
    --border: rgba(255,255,255,0.08);      /* default dividers */
    --border-2: rgba(255,255,255,0.14);    /* slightly stronger border */
    --border-accent: rgba(255,255,255,0.16); /* highlighted borders */
    --green: #22c55e;       /* positive indicators */
    --red: #ef4444;         /* negative indicators */
    --yellow: #f59e0b;      /* warning/watch indicators */
}
```

### To change the accent color (CTA buttons, active states)
Change `--accent`. If you use a color (not white), also update `--accent-light`, `--accent-dim`, and `--border-accent` to tints of the same hue.

Remember: `.btn-accent` uses `color: #080808` (dark text) because the button background is white. If you switch `--accent` to a dark color, change `.btn-accent { color: ... }` to `white`.

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
    --accent: #080808;      /* buttons become black in light sections */
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

A few places bypass the CSS variable system and need manual edits if you're doing a big color change:

| Location | Value | Why hardcoded |
|---|---|---|
| `.banner { background }` | `#080808` | Was `var(--accent)` but that's now white |
| `.btn-accent { color }` | `#080808` | Dark text on white accent button |
| `.mockup-nav-item.active { background }` | `rgba(255,255,255,0.08)` | Neutral white tint |
| `.philosophy-box { background }` | `linear-gradient(#111111, #0d0d0d)` | Dark callout box |
| `.mockup-ai-card { background }` | `linear-gradient(#111111, #0d0d0d)` | Dark AI card in mockup |
| `.ai-demo { background }` | `linear-gradient(#111111, #0b0b0b)` | AI demo box |
| `.pricing-card.featured { background }` | `linear-gradient(#111111, #0d0d0d)` | Dark featured card |
| RevOps compare card (inline HTML, ~line 1518) | `linear-gradient(#111111, #0d0d0d)` | Dark "Selfware" compare card |
| Founder name (inline HTML, ~line 1734) | `color:white` | Sits in a dark section |

---

## Page sections (in order)

```
Banner          — .banner                       always dark
Nav             — nav                           sticky, dark
Hero            — #hero-wrap                    dark, CSS mockup in background
Problem         — #problem.light-section        WHITE background
AI Advisor      — #ai-advisor                   dark
RevOps          — (no id, style=bg-2)           dark
Solution        — #solution                     dark
Features        — #features.light-section       WHITE background
Founder         — #story                        dark
Pricing         — #pricing.light-section        WHITE background
Final CTA       — #apply                        dark
Footer          — footer                        dark
```

---

## Booking link

All "Book a Demo" buttons point to `https://cal.com/jellyfishnocode/selfware`. Search for that URL to find and update all instances.

## Deployment

Push to `master` branch on `jellyfish421/selfware`. GitHub Pages serves it at `selfwaredev.com`.
