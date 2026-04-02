# Audit Checklist

Complete checklist for auditing a generated brandbook. Run this after generation and before delivery.

## Part A: Frontend Design Anti-Patterns

Check every item. Any failure is a CRITICAL issue that must be fixed.

### Typography

- [ ] **No banned fonts**: None of Inter, Arial, Roboto, Helvetica, system-ui, Open Sans, Lato, Poppins, Montserrat, Source Sans Pro, Nunito, Space Grotesk
- [ ] **Multiple font families**: At least 2 distinct font families in use (display ≠ body)
- [ ] **Mono font present**: A dedicated monospace font for labels, code, metadata
- [ ] **Google Fonts loaded with display=swap**: Check `<link>` tags
- [ ] **Google Fonts with preconnect**: `<link rel="preconnect" href="https://fonts.googleapis.com">`
- [ ] **Font fallback stacks**: Every font-family declaration has appropriate fallbacks
- [ ] **No font below 14px**: Smallest text size ≥ 0.875rem (except fine print clearly marked)
- [ ] **Consistent type scale**: Sizes follow a mathematical scale (e.g., 1.25 ratio)
- [ ] **Letter-spacing on display text**: Negative tracking on large headlines
- [ ] **Letter-spacing on caps**: Positive tracking on all-uppercase text

### Colors

- [ ] **No pure white page background**: Page background is NOT `#ffffff` or `#fff`
- [ ] **No pure black text**: Primary text is NOT `#000000` or `#000`
- [ ] **Multi-hue palette**: At least 3 distinct hues (primary + warm accent + cool accent)
- [ ] **Warm accent present**: An accent color in the warm spectrum (amber, orange, coral, gold)
- [ ] **Cool accent present**: An accent color in the cool spectrum (teal, cyan, blue-green)
- [ ] **Semantic colors defined**: Success, warning, error, info — all present and distinct
- [ ] **Light mode surfaces**: Page, card, elevated, border — all defined with brand tinting
- [ ] **Dark mode surfaces**: Deep, base, elevated, border — all defined with brand tinting
- [ ] **Text scales for both modes**: Primary, secondary, tertiary, disabled — for light and dark
- [ ] **WCAG AA contrast**: All text meets 4.5:1 (normal) or 3:1 (large text) on its background
- [ ] **No purple gradient on white**: The #1 AI slop indicator
- [ ] **No monochromatic palette**: Palette is not just light/dark versions of one hue

### Logo & Wordmark

- [ ] **No letter-in-rounded-square**: The most generic AI logo pattern
- [ ] **No gradients on logo/wordmark**: Logo uses flat, solid colors only
- [ ] **Wordmark is typographic**: Uses chosen fonts, not a generic icon
- [ ] **Identity element present**: If the name has a special character, it's visually distinct
- [ ] **Three variants shown**: On-light, on-dark, on-brand-surface
- [ ] **Clear space rules**: Minimum padding around the wordmark is specified
- [ ] **Do/Don't section**: At least 3 dos and 3 don'ts with visual examples

### Layout & Surfaces

- [ ] **No cookie-cutter layout**: Not just Hero → Features → CTA in sequence
- [ ] **Section rhythm**: Alternating light/dark sections for visual variety
- [ ] **Surface texture**: Subtle noise, grain, or pattern overlay (not flat solid colors)
- [ ] **No default framework look**: Doesn't look like unmodified Tailwind/shadcn defaults
- [ ] **Off-white/tinted backgrounds**: Light surfaces have brand-color tinting

### Components

- [ ] **Buttons in both modes**: All button variants shown in light AND dark mode
- [ ] **Cards in both modes**: Card variants in light AND dark mode
- [ ] **Inputs with states**: Default, focus, error, disabled states shown
- [ ] **Tags/badges**: Semantic color tags shown in both modes
- [ ] **Consistent border radius**: All components use the same radius scale
- [ ] **Consistent spacing**: Components use the spacing scale from design tokens

---

## Part B: Accessibility (Web Interface Guidelines)

### Structure

- [ ] **Semantic HTML**: Uses `<header>`, `<main>`, `<nav>`, `<section>`, `<footer>`
- [ ] **Skip link**: First child of `<body>` is a skip-to-content link
- [ ] **Heading hierarchy**: h1 → h2 → h3 — no skipped levels
- [ ] **Landmark roles**: Proper ARIA landmarks (or semantic elements provide them)
- [ ] **Language attribute**: `<html lang="en">` (or appropriate language)

### Visual

- [ ] **color-scheme meta**: `<meta name="color-scheme" content="light dark">`
- [ ] **theme-color meta**: `<meta name="theme-color" content="...">`
- [ ] **focus-visible**: All interactive elements have visible focus indicators
- [ ] **No outline: none**: Focus styles are never removed without replacement
- [ ] **Focus ring specs**: 2px solid, 2px offset, using brand color or high-contrast
- [ ] **prefers-reduced-motion**: All animations wrapped in `@media (prefers-reduced-motion: no-preference)`
- [ ] **prefers-color-scheme**: Auto dark/light switching
- [ ] **Sufficient color contrast**: WCAG AA on all text/background combinations

### Typography

- [ ] **tabular-nums**: `font-variant-numeric: tabular-nums` on numeric data
- [ ] **Antialiased rendering**: `-webkit-font-smoothing: antialiased`
- [ ] **Line length**: Body text max-width between 60–80ch

### Interactive Elements

- [ ] **Input autocomplete**: Form inputs have `autocomplete`, `name`, `type` attributes
- [ ] **Button type**: All `<button>` elements have explicit `type` attribute
- [ ] **Link underlines or clear indication**: Links are distinguishable without color alone
- [ ] **Touch targets**: Interactive elements ≥ 44×44px on mobile

### Print

- [ ] **Print styles**: `@media print` hides navigation, forces light mode
- [ ] **Print-friendly colors**: Dark backgrounds don't print as-is

---

## Part C: Technical Quality

- [ ] **Standalone HTML**: No external CSS/JS dependencies (except Google Fonts)
- [ ] **Responsive**: Works from 320px to 1440px+
- [ ] **Valid HTML**: No obvious structural errors
- [ ] **CSS custom properties**: All design tokens defined as CSS variables
- [ ] **No inline styles**: All styling via CSS classes or custom properties
- [ ] **Organized CSS**: Properties grouped logically (layout, typography, colors, spacing)
- [ ] **SVG noise texture**: Grain/noise uses inline SVG data URI, not external file
- [ ] **Performance**: No unnecessary JavaScript, minimal DOM complexity

---

## Severity Levels

| Level | Meaning | Action |
|-------|---------|--------|
| CRITICAL | Breaks accessibility, uses banned font, or is a clear AI slop indicator | Must fix before delivery |
| HIGH | Reduces quality significantly — missing dark mode, no focus styles | Should fix before delivery |
| MEDIUM | Would improve quality — missing print styles, suboptimal contrast | Fix when possible |
| LOW | Nice to have — additional specimens, more component variants | Note for future iteration |

## Audit Report Format

```
## Audit Results — [Brand Name] Brandbook

### Summary
- CRITICAL: N issues
- HIGH: N issues
- MEDIUM: N issues
- LOW: N issues

### Issues

**[CRITICAL] brandbook.html:42 — Banned font "Inter" in body text**
Replace with recommended alternative from typography guide.

**[HIGH] brandbook.html:156 — Missing focus-visible on nav links**
Add: `a:focus-visible { outline: 2px solid var(--color-primary); outline-offset: 2px; }`

...
```
