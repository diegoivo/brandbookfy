# Design Companion Reference

The design companion is a live HTML preview that transforms into the final brandbook during the brainstorming process. This document explains how to set up, update, and use it.

## Concept

The companion starts as a template with placeholder values and progressively fills in as the user answers discovery questions. By the time discovery is complete, the companion already contains ~80% of the brandbook content and serves as the foundation for the final generation.

This approach has two benefits:
1. The user sees their brand take shape visually, making feedback more concrete
2. The final brandbook generation starts from a mostly-complete base rather than from scratch

## Architecture: Sidebar vs Content

The template separates two visual systems:

- **Sidebar** — independent dark chrome with the "Brandbook" gradient logo. This is the brandbook's own identity (not the brand being created). It stays dark regardless of the brand's token choices.
- **Content** — uses only the brand's own design tokens. Alternating sections use `section-alt` (brand `surface-elevated`) for visual rhythm, never the sidebar's dark colors. This ensures every brand looks correct and unique.

The "Brandbook" wordmark in the sidebar uses a fluid gradient (`primary-light` → `primary-dark`). No word separation — it's one continuous mark.

## Scroll-based Navigation

The template includes an IntersectionObserver script that adds an `.active` class to the sidebar nav link corresponding to the currently visible section. The active link gets a left border accent and elevated background. This works automatically — no manual updates needed.

## Setup

### Step 1: Copy the Template

```
Read: assets/design-companion-template.html
Write to: {project-dir}/brandbook-companion.html
```

### Step 2: Open in Browser

**With browser tools (mcp__claude-in-chrome__):**
1. Create a new tab: `tabs_create_mcp` with `file://{absolute-path}/brandbook-companion.html`
2. Store the tab ID for future updates

**Without browser tools:**
1. Run: `open {project-dir}/brandbook-companion.html`
2. After each update, run `open` again to refresh

## Section-by-Section Update Guide

After each discovery answer, update the corresponding section in the companion HTML.

### After Q1 (Project & Purpose)

Update these CSS custom properties and content:

```css
/* In :root */
--brand-name: '...';
```

Update the header to show the brand name and tagline. Replace the placeholder hero text.

### After Q2 (Brand Archetype)

Update the archetype section:
- Archetype name and icon
- Core traits (3–4 words)
- Personality description (2–3 sentences)

Read `references/brand-archetypes.md` to get the visual cues for the chosen archetype and begin adjusting the overall tone:
- Corner radius (sharp vs rounded)
- Spacing density
- Default theme preference

### After Q3 (Positioning & Tone)

Refine the visual direction based on positioning:
- Adjust weight/boldness of typography
- Set spacing scale (dense vs airy)
- Set motion style hints in the archetype section

### After Q4 (Color Direction)

This is the biggest visual update. Replace ALL color custom properties:

```css
:root {
  /* Core */
  --color-primary-light: #...;
  --color-primary: #...;
  --color-primary-dark: #...;

  /* Accents */
  --color-warm: #...;
  --color-warm-light: #...;
  --color-cool: #...;
  --color-cool-light: #...;

  /* Semantic */
  --color-success: #...;
  --color-warning: #...;
  --color-error: #...;
  --color-info: #...;

  /* Surfaces - Light */
  --surface-page: #...;
  --surface-card: #...;
  --surface-elevated: #...;
  --surface-border: #...;

  /* Surfaces - Dark */
  --surface-dark-deep: #...;
  --surface-dark-base: #...;
  --surface-dark-elevated: #...;
  --surface-dark-border: #...;

  /* Text - Light */
  --text-primary: #...;
  --text-secondary: #...;
  --text-tertiary: #...;
  --text-disabled: #...;

  /* Text - Dark */
  --text-dark-primary: #...;
  --text-dark-secondary: #...;
  --text-dark-tertiary: #...;
  --text-dark-disabled: #...;
}
```

Also update the color palette section to show all swatches with hex values.

**Important — contrast guarantee**: After updating colors, verify that `--text-primary` has at least 4.5:1 contrast ratio against `--surface-page`, `--surface-card`, AND `--surface-elevated`. The type specimens use explicit `color: var(--text-primary)` so they'll always be legible as long as the token values pass contrast checks.

### After Q5 (Typography Mood)

Update font-related properties and load new Google Fonts:

```html
<!-- Update the Google Fonts link -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=...&display=swap" rel="stylesheet">
```

```css
:root {
  --font-display: '...', Georgia, serif;
  --font-heading: '...', system-ui, sans-serif;
  --font-body: '...', system-ui, sans-serif;
  --font-mono: '...', monospace;
}
```

Update the typography section with specimens — actual text rendered in each font at various sizes and weights.

### After Q6 (Identity Element)

Update the wordmark section:
- Render the brand name with the chosen display font
- Highlight the identity element (underscore, dot, etc.) with the primary color
- Show the three variants: on-light, on-dark, on-brand-surface

### After Q7 (Review & Confirm)

Final adjustments based on user feedback. At this point, the companion should look like a near-complete brandbook.

## Updating the Browser

### With browser tools

After editing the HTML file, reload the tab:

```
javascript_tool: location.reload()
```

Or navigate again:
```
navigate: file://{absolute-path}/brandbook-companion.html
```

### Without browser tools

After editing, re-open:
```bash
open {project-dir}/brandbook-companion.html
```

The browser will either reload the existing tab or open a new one.

## Presenting Options

During brainstorming, you may want to show the user 2–3 options for colors or typography. Do this by:

1. Creating a temporary comparison section at the top of the companion
2. Showing options side-by-side with labels (A, B, C)
3. After the user chooses, removing the comparison and applying the chosen option

Example for color options:
```html
<section class="comparison" id="color-options">
  <h2>Color Direction — Pick One</h2>
  <div class="options-grid">
    <div class="option">
      <span class="option-label">A</span>
      <div class="color-preview" style="background: #7c3aed;">Violet</div>
      <p>Mystical, transformative — aligns with Magician archetype</p>
    </div>
    <div class="option">
      <span class="option-label">B</span>
      <div class="color-preview" style="background: #0d9488;">Teal</div>
      <p>Analytical, fresh — aligns with Sage influence</p>
    </div>
    <div class="option">
      <span class="option-label">C</span>
      <div class="color-preview" style="background: #1e40af;">Deep Blue</div>
      <p>Authoritative, deep — balances both archetypes</p>
    </div>
  </div>
</section>
```

## From Companion to Brandbook

When discovery is complete and the user confirms, the companion is already 80% of the brandbook. To produce the final `brandbook.html`:

1. Read the current companion HTML
2. Remove any remaining placeholders or comparison sections
3. Add the missing sections: components (buttons, cards, inputs, tags) and Don't rules
4. Run the full audit (Part A + Part B from `references/audit-checklist.md`)
5. Fix any issues
6. Save as `brandbook.html`

The companion file can be kept as a development artifact or deleted — the brandbook is the deliverable.

## Troubleshooting

**Browser not updating**: Check that the file path is absolute in the browser URL. Relative paths can cause caching issues.

**Fonts not loading**: Google Fonts requires network access. If working offline, use system font fallbacks and note the intended fonts in comments.

**Dark mode flicker**: Ensure `color-scheme` meta tag is set and `prefers-color-scheme` media queries are in place.
