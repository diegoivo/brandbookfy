---
name: brandbookfy
description: Create professional brandbooks and design systems for web projects. Use when the user wants to build a brand identity, design system, brandbook, visual identity, style guide, or establish visual consistency for any project. Also triggers on brand archetypes, color palettes, typography systems, design tokens, or when starting a new project that needs visual identity. Use this whenever someone says "create a brandbook", "design system", "brand identity", "visual identity", "style guide", "design tokens", "brand colors", "brand typography", or is starting a new project where visual identity would add value. Even partial matches like "pick colors for my project" or "what fonts should I use" should trigger this skill.
---

# Brandbook Design System

Create distinctive, production-grade brandbooks that avoid generic "AI slop" aesthetics. This skill guides the full journey from brand discovery to an exportable design system.

## What You Produce

| File | Purpose |
|------|---------|
| `brandbook.html` | Visual brandbook for presentation — standalone, no external deps except Google Fonts |
| `design-tokens.json` | Colors, fonts, spacing, radii — structured for implementation |
| `BRAND.md` | Text summary for LLM context in future sessions |

## Process

```
Discovery → Design Companion → Generation → Audit → Export
```

1. **Discovery**: Guided brainstorming — one question at a time
2. **Design Companion**: Live HTML preview updated as decisions are made
3. **Generation**: Full brandbook HTML with all sections
4. **Audit**: Check against web interface guidelines + frontend design anti-patterns
5. **Export**: Produce all three output files

---

## Phase 1: Discovery

**Language**: Detect the user's language from their first message and conduct ALL discovery questions in that language. The brandbook output files (HTML, JSON, BRAND.md) stay in English, but the brainstorming conversation adapts to the user.

Ask these questions **one at a time**. Wait for the user's answer before moving on. After each answer, update the design companion if browser tools are available.

### Question Flow

**Q1 — Project & Purpose**
"What's the project name and what does it do? Who is it for?"
→ Establishes context, audience, and naming constraints.

**Q2 — Brand Archetype**
"Which brand personality resonates most?"
Present the 12 archetypes with one-line descriptions. Read `references/brand-archetypes.md` for the full list with visual cues. Let the user pick one or describe a blend.
→ Establishes personality traits, emotional tone, and visual direction.

**Q3 — Positioning & Tone**
"Where does the brand sit on these spectrums?"
- Premium ←→ Accessible
- Technical ←→ Approachable
- Bold ←→ Subtle
- Playful ←→ Serious
→ Calibrates the entire aesthetic — colors, type weight, spacing, motion.

**Q4 — Color Direction**
"What color family feels right? Any colors to avoid?"
Suggest 2–3 candidate palettes based on archetype + positioning. Show them in the companion if available. Read `references/color-system.md` for how to build a complete palette from a seed.
→ Seeds the full color system (core, accents, semantic, surfaces).

**Q5 — Typography Mood**
"What typographic character fits the brand?"
Offer these directions with example pairings:
- Elegant/editorial — serif display + geometric sans body
- Modern/geometric — distinctive sans display + clean sans body
- Technical/precise — mono accents + humanist sans body
- Warm/humanist — rounded sans + friendly serif display
Read `references/typography-guide.md` for specific font recommendations. Show specimens in the companion.
→ Defines the type system (display, heading, body, mono).

**Q6 — Identity Element**
"Does the name have a special character or element that could become part of the visual identity?"
Examples: underscore in `Rankbase_`, dot in `Layer.ai`, slash in `Next/js`, brackets in `[dev]`
→ Finds the distinctive hook that makes the wordmark memorable.

**Q7 — Review & Confirm**
Summarize all decisions in a structured table. Ask the user to confirm or adjust before generation.

---

## Phase 2: Design Companion

The design companion is a live HTML preview that visualizes brand decisions as they're made during discovery. It makes the brainstorming tangible — the user sees their brand take shape in real time.

### Mode Selection

| Context | Behavior |
|---------|----------|
| Browser tools available (`mcp__claude-in-chrome__*`) | Full interactive companion with live updates |
| No browser tools | Generate a static companion HTML, open with `open` command, regenerate after each major decision |
| Text-only session | Skip companion entirely, proceed with text-based brainstorming |

### Setup

1. Read the template from `assets/design-companion-template.html`
2. Copy it to the project directory as `brandbook-companion.html`
3. Open it in a browser tab
4. After each discovery answer, update the relevant CSS custom properties and section content
5. Reload the browser to show changes

The companion progressively transforms into the brandbook. By the time discovery is complete, it already contains 80% of the final brandbook content.

Read `references/design-companion.md` for detailed section-by-section update instructions.

---

## Phase 3: Generation

After discovery, generate the full brandbook as a standalone HTML file.

### Brandbook Sections

```
01 — Brand Archetype
     Personality name, core traits (3–4 words), emotional tone,
     voice guidelines (how the brand speaks)

02 — Logo & Wordmark
     Primary wordmark rendered with chosen fonts + identity element
     Variants: on-light, on-dark, on-brand-surface
     Clear space rules (use the cap-height as minimum padding)
     Do/Don't examples — minimum 3 each, with visual demos

03 — Color Palette
     Core: primary (light, base, dark)
     Accents: warm (base, light) + cool (base, light)
     Semantic: success, warning, error, info
     Surfaces light: page, card, elevated, border
     Surfaces dark: deep, base, elevated, border
     Text light: primary, secondary, tertiary, disabled
     Text dark: primary, secondary, tertiary, disabled
     Each swatch shows hex, usage label, and WCAG contrast ratio

04 — Typography
     Display: family, weight, sizes, line-height, letter-spacing, specimen
     Heading: family, weight scale (h1–h6), specimen
     Body: family, weight, sizes, line-height, specimen
     Mono: family, weight, use cases, specimen
     Type scale table with px/rem values

05 — Components
     Buttons: primary, secondary, outline, ghost, destructive — light + dark
     Cards: default, interactive (hover), featured — light + dark
     Inputs: text, select, textarea with states (default, focus, error, disabled) — light + dark
     Tags/Badges: all semantic colors — light + dark

06 — Don't (Negative Rules)
     Visual demonstrations of what NOT to do:
     - Never stretch or rotate the wordmark
     - Never apply gradients to the logo
     - Never use unapproved color combinations
     - Never set body text below 14px/0.875rem
     - Never remove focus indicators
     - Never use the brand fonts for decorative purposes at extreme sizes
```

### Anti-AI-Slop Rules (enforce during generation)

These are non-negotiable. Every brandbook must pass these checks:

**Typography — NEVER use these fonts:**
Inter, Arial, Roboto, Helvetica, system-ui, Open Sans, Lato, Poppins, Montserrat, Source Sans Pro, Nunito, Space Grotesk.
Instead: choose from `references/typography-guide.md`. Always use at least 3 font families (display, body, mono).

**Colors — NEVER do these:**
- Pure white `#ffffff` or `#fff` as page background — always tint with primary hue (e.g., `#faf8fc` for violet)
- Pure black `#000000` or `#000` as text — always use brand-tinted near-black
- Monochromatic palette (only light/dark of one hue) — always include warm AND cool accents
- Purple gradient on white background — the #1 AI slop signal
- Same hue for primary and accent colors

**Logo — NEVER do these:**
- Letter inside a rounded square — the most generic AI logo
- Gradients on the wordmark — logo must always be flat, solid color
- Generic icon + name — use a typographic wordmark with the identity element instead

**Layout — NEVER do these:**
- Cookie-cutter Hero → Features → CTA sequence
- Flat solid backgrounds with no texture — always add subtle noise/grain
- Same background for every section — alternate `surface-page` and `surface-elevated`

**Components — NEVER do these:**
- Default shadcn/Tailwind appearance — always customize with brand tokens
- Missing dark mode variants — every component shows in both modes
- Missing states (focus, hover, error, disabled) on inputs

### Technical Requirements

Every generated brandbook HTML must include:

**Meta & Theme:**
```html
<meta name="color-scheme" content="light dark">
<meta name="theme-color" content="{primary-base}">
```

**Accessibility:**
- Skip link as first child of `<body>`
- `focus-visible` outlines on ALL interactive elements (2px solid, 2px offset)
- `prefers-reduced-motion: reduce` — disable all animations and transitions
- `prefers-color-scheme` — auto-switch light/dark
- Semantic HTML: `<header>`, `<main>`, `<nav>`, `<section>`, `<footer>`
- `font-variant-numeric: tabular-nums` on numeric content
- WCAG AA contrast on all text (4.5:1 normal, 3:1 large)
- Never use `outline: none` without a visible focus replacement

**Visual Polish:**
- Google Fonts via `<link>` with `display=swap` and `preconnect`
- CSS custom properties for ALL design tokens
- Subtle noise/grain texture overlay on surfaces (CSS `background-image` with SVG data URI)
- Section rhythm: alternate between `surface-page` and `surface-elevated` — the sidebar owns the dark chrome, content stays in brand token space
- Off-white page background (never pure `#ffffff`) — tint with primary hue
- "Brandbook" logo in sidebar uses fluid gradient (`primary-light` → `primary-dark`), no word separation
- Scroll-based active section highlighting in sidebar nav via IntersectionObserver

**Structure:**
- All CSS inline in `<style>` — no external stylesheets
- All interactivity via vanilla JS — no frameworks
- Print styles: hide navigation, force light mode
- Responsive: readable on mobile (min 320px)

**Adaptability — The brandbook's design system overrides the template defaults:**
- Every visual property derives from CSS custom properties that get replaced during brainstorming
- The sidebar is independent chrome — its dark theme persists regardless of brand tokens
- The content area NEVER uses the sidebar's dark surface colors — it only uses brand surface tokens (`surface-page`, `surface-card`, `surface-elevated`)
- Dark mode preview panels within components are self-contained (`mode-preview-dark`) and don't leak into the layout
- All text in specimens, cards, and components must use explicit `color: var(--text-primary)` to guarantee contrast on any surface — never rely on inheritance alone

---

## Phase 4: Audit

Run a two-part audit before delivering the brandbook. Fix all issues before showing results.

### Part A — Web Interface Guidelines

Fetch the latest guidelines:
```
https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md
```
Check the brandbook HTML against all rules. Report in `file:line` format.

### Part B — Frontend Design Anti-Patterns

Read `references/audit-checklist.md` and verify every item. This catches the "AI slop" patterns that make generated designs look generic and forgettable.

### Remediation

Fix all CRITICAL and HIGH issues before delivery. MEDIUM issues should be fixed when possible. Present the audit summary to the user along with the brandbook.

---

## Phase 5: Export

### `brandbook.html`
The audit-clean brandbook from Phase 3.

### `design-tokens.json`
```json
{
  "brand": {
    "name": "...",
    "archetype": "...",
    "tagline": "..."
  },
  "colors": {
    "core": {
      "primary": { "light": "#...", "base": "#...", "dark": "#..." }
    },
    "accent": {
      "warm": { "base": "#...", "light": "#..." },
      "cool": { "base": "#...", "light": "#..." }
    },
    "semantic": { "success": "#...", "warning": "#...", "error": "#...", "info": "#..." },
    "surface": {
      "light": { "page": "#...", "card": "#...", "elevated": "#...", "border": "#..." },
      "dark": { "deep": "#...", "base": "#...", "elevated": "#...", "border": "#..." }
    },
    "text": {
      "light": { "primary": "#...", "secondary": "#...", "tertiary": "#...", "disabled": "#..." },
      "dark": { "primary": "#...", "secondary": "#...", "tertiary": "#...", "disabled": "#..." }
    }
  },
  "typography": {
    "display": { "family": "...", "weight": 400, "letterSpacing": "..." },
    "heading": { "family": "...", "weights": [500, 600, 700] },
    "body": { "family": "...", "weight": 400, "lineHeight": 1.6 },
    "mono": { "family": "...", "weight": 400 }
  },
  "spacing": { "xs": "0.25rem", "sm": "0.5rem", "md": "1rem", "lg": "1.5rem", "xl": "2rem", "2xl": "3rem" },
  "radii": { "sm": "0.25rem", "md": "0.5rem", "lg": "0.75rem", "xl": "1rem", "full": "9999px" }
}
```

### `BRAND.md`
```markdown
# [Brand Name] — Brand Guidelines

## Archetype
[Name]: [One-line description of personality]

## Visual Identity
- **Wordmark**: [Description including identity element]
- **Display font**: [Name + weight]
- **Heading font**: [Name]
- **Body font**: [Name]
- **Mono font**: [Name]

## Color System
- **Primary**: [hex] (light / base / dark)
- **Warm accent**: [hex]
- **Cool accent**: [hex]
- **Light surfaces**: page [hex], card [hex], elevated [hex]
- **Dark surfaces**: deep [hex], base [hex], elevated [hex]

## Key Rules
- [3–5 most important brand rules]

## Anti-Patterns
- [3–5 things to never do with this brand]
```

---

## Critical Anti-Patterns

These patterns make designs look AI-generated. Avoid at all costs:

| Category | Anti-Pattern | Why It Fails |
|----------|-------------|--------------|
| Typography | Inter, Arial, Roboto, system fonts | Generic — flagged as AI output by design-aware audiences |
| Typography | Single font family for everything | Destroys visual hierarchy |
| Colors | Monochromatic palette (one hue) | Flat, no emotional range or functional differentiation |
| Colors | Pure white `#ffffff` as page background | Generic — lacks brand warmth |
| Colors | Purple gradient on white | The most common AI slop indicator |
| Logo | Letter in rounded square | The default AI-generated SaaS logo |
| Logo | Gradients on wordmark | Instantly dated, can't be used in all contexts |
| Layout | Hero → Features → CTA | Cookie-cutter, indistinguishable from templates |
| Surfaces | Flat solid backgrounds | Sterile, lacks depth and texture |
| Components | Default shadcn/Tailwind look | Recognizable as unmodified framework defaults |

See `references/audit-checklist.md` for the exhaustive list.

---

## Font Recommendations

Never use: Inter, Arial, Roboto, Helvetica, system-ui, Open Sans, Lato, Poppins, Montserrat, Source Sans Pro.

Recommended alternatives (read `references/typography-guide.md` for full pairings):

| Role | Options |
|------|---------|
| Display (serif) | Instrument Serif, DM Serif Display, Playfair Display, Fraunces |
| Display (sans) | Plus Jakarta Sans, Outfit, General Sans, Cabinet Grotesk |
| Body | Plus Jakarta Sans, Manrope, Satoshi, Geist Sans, Switzer |
| Mono | JetBrains Mono, Geist Mono, IBM Plex Mono, Fira Code |
