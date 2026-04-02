# Color System Reference

How to build a complete, functional color palette from a single seed color.

## Palette Structure

Every brandbook needs these color groups:

```
Core
├── Primary light    (tints for backgrounds, hover states)
├── Primary base     (the main brand color)
└── Primary dark     (shadows, pressed states, text on light)

Accents
├── Warm accent      (energy, highlights, CTAs — amber, orange, coral, gold)
│   ├── base
│   └── light
└── Cool accent      (data, metrics, links — teal, cyan, blue-green)
    ├── base
    └── light

Semantic
├── Success          (green family — not the same as cool accent)
├── Warning          (amber/yellow family)
├── Error            (red family — distinct from warm accent)
└── Info             (blue family)

Surfaces — Light Mode
├── Page             (off-white tinted with primary hue — NEVER pure #ffffff)
├── Card             (slightly lighter than page, or white with subtle tint)
├── Elevated         (raised elements — slightly darker than card)
└── Border           (subtle, low-contrast divider)

Surfaces — Dark Mode
├── Deep             (deepest background — near-black tinted with primary)
├── Base             (main dark background)
├── Elevated         (raised surfaces — lighter than base)
└── Border           (subtle light divider)

Text — Light Mode
├── Primary          (near-black — not pure #000000)
├── Secondary        (muted — for descriptions, metadata)
├── Tertiary         (even more muted — for hints, placeholders)
└── Disabled         (lowest contrast — still meets 3:1 for large text)

Text — Dark Mode
├── Primary          (near-white — not pure #ffffff)
├── Secondary        (muted light)
├── Tertiary         (dim)
└── Disabled         (lowest visibility)
```

## Building from a Seed Color

### Step 1: Choose the primary base

The seed color from the user's preference. Adjust saturation and lightness for screen use:
- HSL lightness between 35–55% for the base (readable on both light and dark backgrounds)
- Saturation between 60–90% (vivid but not neon)

### Step 2: Generate primary light and dark

- **Light**: Increase lightness by 15–20%, reduce saturation by 5–10%
- **Dark**: Decrease lightness by 15–20%, increase saturation by 5%

### Step 3: Choose accents

Accents should be **different hues** from the primary — not just lighter/darker versions.

**Warm accent**: Pick a hue 60–120° away from primary on the warm side of the wheel.
- If primary is violet (270°) → warm accent around amber (40°) or coral (15°)
- If primary is blue (220°) → warm accent around orange (30°) or gold (45°)
- If primary is green (140°) → warm accent around terracotta (15°) or magenta (330°)

**Cool accent**: Pick a hue 60–120° away on the cool side.
- If primary is violet → cool accent around teal (175°) or cyan (190°)
- If primary is red → cool accent around blue (220°) or teal (175°)
- If primary is green → cool accent around blue-violet (260°)

### Step 4: Define semantic colors

Use universally recognized associations:
- **Success**: Green (hue 140–160°), saturation 60–80%, lightness 40–50%
- **Warning**: Amber/yellow (hue 35–50°), saturation 80–95%, lightness 45–55%
- **Error**: Red (hue 0–10°), saturation 70–85%, lightness 45–55%
- **Info**: Blue (hue 200–220°), saturation 60–80%, lightness 45–55%

Semantic colors should feel like they belong to the palette — adjust saturation and warmth to match the brand's overall tone.

### Step 5: Build surfaces

**Light mode surfaces:**
- Page: Take primary hue, set saturation to 10–20%, lightness to 97–98%. This creates an off-white with brand warmth.
- Card: Slightly lighter or use `#ffffff` with very subtle tint
- Elevated: 2–3% darker than card
- Border: Primary hue, 10% saturation, 85–90% lightness

**Dark mode surfaces:**
- Deep: Primary hue, 30–50% saturation, 3–5% lightness (near-black with brand tint)
- Base: Primary hue, 25–40% saturation, 7–10% lightness
- Elevated: Primary hue, 20–35% saturation, 12–16% lightness
- Border: Primary hue, 15–25% saturation, 20–25% lightness

### Step 6: Define text scales

**Light mode text:**
- Primary: Primary hue, 15–25% saturation, 8–12% lightness (near-black, brand-tinted)
- Secondary: Primary hue, 10–15% saturation, 35–45% lightness
- Tertiary: Primary hue, 8–12% saturation, 55–60% lightness
- Disabled: Primary hue, 5–10% saturation, 70–75% lightness

**Dark mode text:**
- Primary: Primary hue, 5–15% saturation, 92–96% lightness
- Secondary: Primary hue, 8–12% saturation, 70–75% lightness
- Tertiary: Primary hue, 5–10% saturation, 55–60% lightness
- Disabled: Primary hue, 5–8% saturation, 40–45% lightness

## WCAG Contrast Requirements

All text must meet WCAG AA:
- Normal text (< 18px or < 14px bold): **4.5:1** contrast ratio
- Large text (≥ 18px or ≥ 14px bold): **3:1** contrast ratio
- UI components and graphical objects: **3:1**

Check every combination of text color on surface color. Use the formula:
```
contrastRatio = (L1 + 0.05) / (L2 + 0.05)
```
where L1 is the relative luminance of the lighter color and L2 the darker.

## Common Mistakes

- **Pure black text on pure white**: Too harsh. Use brand-tinted near-black on brand-tinted off-white.
- **Same hue for primary and accent**: Palette feels monochromatic. Accents need hue contrast.
- **Forgetting dark mode surfaces**: Dark mode is not just "invert everything." Dark surfaces need their own carefully crafted scale.
- **Semantic colors clashing with brand**: If primary is red, the error color needs to be a clearly different red (more orange or more pink) to avoid confusion.
- **Over-saturated surfaces**: Surfaces should be nearly neutral with just a hint of brand color.
