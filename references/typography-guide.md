# Typography Guide

Font recommendations for brandbooks. Every suggestion here is available on Google Fonts with `display=swap`.

## Banned Fonts

Never use these in a brandbook — they signal generic/AI-generated design:

| Font | Why It's Banned |
|------|----------------|
| Inter | Overused default in every AI-generated site |
| Arial | System font, zero personality |
| Roboto | Android default, feels generic on web |
| Helvetica | Classic but signals "didn't choose a font" |
| system-ui | Not a design choice, it's a fallback |
| Open Sans | The 2015 default, dated |
| Lato | Overused in templates |
| Poppins | The new "generic modern" |
| Montserrat | Overused in SaaS/startup templates |
| Source Sans Pro | Google's corporate default |
| Nunito / Nunito Sans | Overused in dashboards and admin panels |
| Space Grotesk | Rapidly becoming the new "AI font" |

## Recommended Fonts by Role

### Display Fonts (Serif)

For headlines, hero text, brand statements. These add character and editorial quality.

| Font | Character | Best For | Weight |
|------|-----------|----------|--------|
| **Instrument Serif** | Elegant, editorial, slightly quirky | Premium, editorial, Magician/Lover archetypes | 400 |
| **DM Serif Display** | Classic, authoritative, warm | Traditional luxury, Ruler/Sage archetypes | 400 |
| **Playfair Display** | High contrast, refined | Fashion, editorial, premium services | 400–900 |
| **Fraunces** | Soft, wonky, characterful | Friendly premium, Creator/Jester archetypes | 100–900 (variable) |
| **Libre Baskerville** | Bookish, trustworthy | Publishing, education, Sage archetype | 400, 700 |
| **Cormorant** | Delicate, elegant, high contrast | Luxury, beauty, Lover archetype | 300–700 |
| **Newsreader** | Editorial, readable, classic | Content-heavy, magazine, Sage archetype | 200–800 (variable) |

### Display Fonts (Sans-Serif)

For modern, geometric, or technical brand personalities.

| Font | Character | Best For | Weight |
|------|-----------|----------|--------|
| **Plus Jakarta Sans** | Geometric, modern, clean | Tech, SaaS, Magician/Creator archetypes | 200–800 |
| **Outfit** | Geometric, friendly, distinctive | Startups, consumer apps, Explorer archetype | 100–900 |
| **General Sans** | Neutral with character | Versatile — works for most archetypes | 200–700 |
| **Cabinet Grotesk** | Bold, confident, geometric | Bold brands, Hero/Outlaw archetypes | 100–900 |
| **Sora** | Geometric, futuristic, clean | Tech, AI, data — Sage/Magician archetypes | 100–800 |
| **Bricolage Grotesque** | Quirky, expressive, varied | Creative brands, Jester/Creator archetypes | 200–800 (variable) |
| **Unbounded** | Rounded, playful, bold | Gaming, kids, Jester/Innocent archetypes | 200–900 |

### Body Fonts

Readability is paramount. These are excellent for long-form text.

| Font | Character | Pairs Well With | Weight |
|------|-----------|----------------|--------|
| **Plus Jakarta Sans** | Clean, modern, geometric | Instrument Serif, DM Serif Display | 200–800 |
| **Manrope** | Humanist, warm, readable | Any serif display, Outfit | 200–800 |
| **Geist Sans** | Technical precision, modern | Geist Mono, any serif | 100–900 |
| **Switzer** | Neutral, professional, clean | Most display fonts | 100–900 |
| **Satoshi** | Geometric, contemporary | Cabinet Grotesk, Fraunces | 300–900 |
| **Albert Sans** | Clean, geometric, versatile | Serif displays, Sora | 100–900 |
| **Figtree** | Friendly, geometric, readable | Friendly serifs, Bricolage | 300–900 |

### Monospace Fonts

For code, labels, metadata, and technical elements.

| Font | Character | Best For |
|------|-----------|----------|
| **JetBrains Mono** | Technical, precise, wide | Developer tools, SaaS dashboards, labels |
| **Geist Mono** | Modern, clean, compact | Modern tech, pairs with Geist Sans |
| **IBM Plex Mono** | Professional, classic | Enterprise, professional services |
| **Fira Code** | Ligatures, playful tech | Developer-focused brands |
| **Source Code Pro** | Neutral, readable | General purpose mono needs |

## Recommended Pairings

These are tested combinations that work well together:

### Premium/Editorial
```
Display: Instrument Serif 400
Heading: Plus Jakarta Sans 600–700
Body:    Plus Jakarta Sans 400
Mono:    JetBrains Mono 400
```

### Modern/Tech
```
Display: Outfit 700–800
Heading: Outfit 500–600
Body:    Manrope 400
Mono:    Geist Mono 400
```

### Bold/Confident
```
Display: Cabinet Grotesk 800
Heading: Cabinet Grotesk 600
Body:    Satoshi 400
Mono:    IBM Plex Mono 400
```

### Warm/Approachable
```
Display: Fraunces 600 (variable)
Heading: Figtree 600
Body:    Figtree 400
Mono:    Fira Code 400
```

### Classic/Authoritative
```
Display: DM Serif Display 400
Heading: Albert Sans 600
Body:    Albert Sans 400
Mono:    IBM Plex Mono 400
```

### Playful/Creative
```
Display: Bricolage Grotesque 700
Heading: Bricolage Grotesque 500
Body:    Manrope 400
Mono:    Fira Code 400
```

## Type Scale

Use a consistent scale for all typography. The recommended base is `1rem = 16px`.

### Modular Scale (1.250 — Major Third)

```
6xl:  3.815rem  (61.04px) — Hero headlines
5xl:  3.052rem  (48.83px) — Section heroes
4xl:  2.441rem  (39.06px) — Page titles
3xl:  1.953rem  (31.25px) — Section headings
2xl:  1.563rem  (25.00px) — Subsection headings
xl:   1.25rem   (20.00px) — Large body, lead text
base: 1rem      (16.00px) — Body text
sm:   0.8rem    (12.80px) — Captions, labels
xs:   0.64rem   (10.24px) — Fine print (use sparingly)
```

### Line Height

- Display/Hero: 1.1–1.2 (tight)
- Headings: 1.2–1.3
- Body: 1.5–1.7 (comfortable reading)
- UI labels: 1.3–1.4

### Letter Spacing

- Display (large): -0.02em to -0.04em (tighten for presence)
- Headings: -0.01em to -0.02em
- Body: 0 (default)
- All-caps labels: 0.05em to 0.1em (loosen for readability)
- Mono: 0 (already spaced for alignment)

## CSS Best Practices

```css
/* Always use font-display: swap via Google Fonts link */
/* <link href="...&display=swap" rel="stylesheet"> */

/* Define font stacks with appropriate fallbacks */
--font-display: 'Instrument Serif', Georgia, 'Times New Roman', serif;
--font-heading: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;
--font-body: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;

/* Tabular numbers for data */
.numeric { font-variant-numeric: tabular-nums; }

/* Proper text rendering */
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}

/* Responsive type scale */
html { font-size: clamp(15px, 1vw + 12px, 18px); }
```
