# Lattice — Typography

## Design Intent

Lattice's type system uses three voices that work together to create a Swiss minimalist identity with clinical precision and editorial warmth. The system is inspired by AG1's type hierarchy (serif headlines, mono data labels, clean sans body) filtered through a stricter Swiss International Style discipline.

Typography is the primary vehicle for brand personality. The restrained color palette means type weight, size, spacing, and family selection carry most of the expressive load.

---

## Font Families

Three families. Three distinct roles. No overlap.

```css
:root {
  --font-serif: 'IBM Plex Serif', Georgia, 'Times New Roman', serif;
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-mono: 'IBM Plex Mono', 'SF Mono', 'Consolas', monospace;
}
```

### IBM Plex Serif — The Authority Voice

Used for hero headlines and select section headlines where the site needs to shift register and make a definitive claim. This is the voice that says "we are the only patented medical food for migraine."

Rules:
- **Hero headline only, plus 1–2 key section headlines per page.** The moment serif appears everywhere, it loses its power.
- Weight range: Light (300) to Regular (400). Never bold. The size does the work.
- Always paired with a Plex Mono eyebrow above or an Inter subline below — never standalone without context.

### Inter — The Workhorse

Used for everything that needs to be read comfortably and feel neutral. Body copy, navigation, buttons, form elements, product descriptions, prices, UI labels, section subheadlines, card text.

Rules:
- Weight range: Regular (400) for body, Medium (500) for UI labels and subheads, Semi-bold (600) for emphasis within body text. Never bold (700) in body copy.
- This is the default. If you're unsure which font to use, it's Inter.

### IBM Plex Mono — The Clinical Voice

Used for eyebrow/kicker text, data labels, dosage callouts, spec lists, patent numbers, certifications, and anywhere the content needs to signal "this is measurable, verifiable, precise."

Rules:
- **Always uppercase.** Always letterspaced (`letter-spacing: 0.1em` minimum).
- **Always small.** Never larger than `--text-sm`. The mono voice is quiet and technical — it whispers precision, it doesn't shout.
- Weight: Regular (400) only.
- Used for eyebrows above section headlines, ingredient manifest labels, stat descriptors, metadata.

---

## Type Scale — Fluid, Algorithmically Derived

The type scale is generated from a modular scale with two anchor points. At the minimum viewport (320px), the base size is 15px with a 1.200 ratio (minor third). At the maximum viewport (1440px), the base size is 17px with a 1.275 ratio. Between those viewpoints, every size interpolates linearly using `clamp()`.

This means the **ratio itself scales fluidly** — on small screens the difference between body and headline is compressed; on large screens the headlines pull away proportionally. Every step maintains a mathematically consistent relationship to every other step at every viewport width. This is the Utopia methodology.

### Scale Configuration

```
Min viewport:   320px
Max viewport:   1440px
Min base size:  15px   (0.9375rem)
Max base size:  17px   (1.0625rem)
Min ratio:      1.200  (minor third)
Max ratio:      1.275
Steps:          -2 to +5 (8 total sizes)
```

### Generated Scale

```css
:root {
  /* Step -2: Fine print, legal, metadata */
  --text-xs: clamp(0.651rem, 0.622rem + 0.146vw, 0.694rem);         /* ~10.4–11.1px */

  /* Step -1: Mono labels, captions, button text */
  --text-sm: clamp(0.781rem, 0.746rem + 0.179vw, 0.885rem);         /* ~12.5–14.2px */

  /* Step 0 (base): Body copy */
  --text-base: clamp(0.938rem, 0.893rem + 0.223vw, 1.063rem);       /* 15–17px */

  /* Step +1: Large body, card headings, sublines */
  --text-lg: clamp(1.125rem, 1.056rem + 0.345vw, 1.355rem);         /* ~18–21.7px */

  /* Step +2: Subheadlines, within-section headings */
  --text-xl: clamp(1.35rem, 1.243rem + 0.536vw, 1.728rem);          /* ~21.6–27.6px */

  /* Step +3: Section headlines */
  --text-2xl: clamp(1.62rem, 1.459rem + 0.804vw, 2.203rem);         /* ~25.9–35.2px */

  /* Step +4: Major section headlines, hero subheads */
  --text-3xl: clamp(1.944rem, 1.709rem + 1.175vw, 2.809rem);        /* ~31.1–44.9px */

  /* Step +5: Hero headline, display type */
  --text-4xl: clamp(2.333rem, 1.999rem + 1.67vw, 3.583rem);         /* ~37.3–57.3px */

  /* Stat numbers — separate from the modular scale, hand-sized for impact */
  --text-stat: clamp(3rem, 2rem + 5vw, 6rem);                        /* 48–96px */
}
```

### Why This Matters

With hand-tuned `clamp()` values, the ratio between `--text-2xl` and `--text-3xl` might be 1.3× at 320px but 1.4× at 900px — the scale drifts at intermediate viewports. With an algorithmically derived scale, that ratio is consistent at every width. The visual hierarchy stays proportionally correct on every device, not just at the two endpoints you tested.

---

## The Two-Axis Typography System

### The Problem This Solves

In most themes, heading styles are tightly coupled to HTML elements. An `h2` always looks one way, so when a designer needs an `h2` at a smaller size (say, inside a card), the developer creates `.card-h2` or `.h2--small`. Multiply this across every context and you end up with dozens of one-off classes: `.hero-h2`, `.sidebar-h3`, `.modal-title`, `.card-title-sm`.

Lattice separates two concerns:

1. **Semantic level** — what the element IS in the document hierarchy (h1, h2, h3, p). This is for accessibility, SEO, and document outline. It carries no visual opinion.
2. **Visual size** — how the element LOOKS. This is a separate class that can be applied to any element.

This means you can write an `<h2>` that looks like an `h4`, or a `<p>` that looks like large body text, without creating context-specific classes.

### Heading Size Classes

These classes control visual presentation only. They do not imply any HTML element.

```css
.heading-display {
  /* The hero statement — largest heading size */
  font-family: var(--font-serif);
  font-size: var(--text-4xl);
  font-weight: var(--weight-light);
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-tight);
}

.heading-1 {
  /* Primary section headlines — large, impactful */
  font-family: var(--font-sans);
  font-size: var(--text-3xl);
  font-weight: var(--weight-medium);
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-normal);
}

.heading-1--serif {
  /* Editorial variant of heading-1 — for 1–2 key sections per page */
  font-family: var(--font-serif);
  font-size: var(--text-3xl);
  font-weight: var(--weight-light);
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-tight);
}

.heading-2 {
  /* Standard section headlines */
  font-family: var(--font-sans);
  font-size: var(--text-2xl);
  font-weight: var(--weight-medium);
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-normal);
}

.heading-3 {
  /* Subsection heads, card group titles */
  font-family: var(--font-sans);
  font-size: var(--text-xl);
  font-weight: var(--weight-medium);
  line-height: var(--leading-snug);
  letter-spacing: var(--tracking-normal);
}

.heading-4 {
  /* Card titles, ingredient names, feature labels */
  font-family: var(--font-sans);
  font-size: var(--text-lg);
  font-weight: var(--weight-medium);
  line-height: var(--leading-snug);
  letter-spacing: var(--tracking-normal);
}

.heading-5 {
  /* Smallest heading — tight labels, metadata headings */
  font-family: var(--font-sans);
  font-size: var(--text-base);
  font-weight: var(--weight-medium);
  line-height: var(--leading-snug);
  letter-spacing: var(--tracking-wide);
}
```

### How to Use: Semantic + Visual

The HTML element defines meaning. The class defines appearance.

```html
<!-- Hero: semantically h1, visually display-size serif -->
<h1 class="heading-display">Your brain's preferred fuel</h1>

<!-- Section headline: semantically h2, visually heading-1 (large) -->
<h2 class="heading-1">What's Inside?</h2>

<!-- Section headline that needs editorial weight: h2 with serif variant -->
<h2 class="heading-1--serif">The science of ketone bodies</h2>

<!-- Same-level h2 but in a tighter context (e.g., inside a two-column split): visually smaller -->
<h2 class="heading-2">Clinically studied ingredients</h2>

<!-- Card title: semantically h3, but visually at heading-4 size -->
<h3 class="heading-4">Magnesium Bisglycinate</h3>

<!-- Sidebar or footer heading: semantically h3, visually at heading-5 size -->
<h3 class="heading-5">Resources</h3>
```

The key insight: an `<h2 class="heading-3">` is perfectly valid and common. You're not breaking the document outline (it's still an h2 for accessibility), but you're sizing it for a context where the full heading-1 or heading-2 treatment would be too large.

---

## Type Roles

The fluid scale defines size relationships.
Type roles define what practitioners actually reach for.

Lattice should expose role language before it exposes raw size language. The role is the API. The scale is the engine behind it.

### Core Roles

| Role | Purpose | Default class mapping |
|------|---------|------------------------|
| display | Hero statement | `.heading-display` |
| headline-xl | Major section headline | `.heading-1` or `.heading-1--serif` |
| headline-lg | Standard section headline | `.heading-2` |
| headline-md | Subsection headline | `.heading-3` |
| headline-sm | Card or utility headline | `.heading-4` |
| headline-xs | Tight metadata heading | `.heading-5` |
| body-lg | Premium intro or pull copy | `.text-lg` |
| body | Default paragraph copy | `.text-base` |
| body-sm | Compact paragraph copy | `.text-sm` |
| caption | Fine print and legal support | `.text-xs` |
| eyebrow | Technical context label | `.mono-label` |
| meta | Compact technical label | `.mono-caption` |
| stat | Quantitative display number | `.stat-number` |
| label | UI field or control label | `.text-label` |

This keeps people from naming classes after contexts like `card-title-sm` or `footer-copy`.

### Text Size Classes

For body text/paragraphs, the same principle applies. The `<p>` element is always semantic, but the visual size varies.

```css
.text-xl {
  font-family: var(--font-sans);
  font-size: var(--text-xl);
  font-weight: var(--weight-regular);
  line-height: var(--leading-snug);
}

.text-lg {
  /* Hero sublines, featured descriptions, pull quotes */
  font-family: var(--font-sans);
  font-size: var(--text-lg);
  font-weight: var(--weight-regular);
  line-height: var(--leading-normal);
}

.text-base {
  /* Default body copy — this is the baseline, applied by default to <p> */
  font-family: var(--font-sans);
  font-size: var(--text-base);
  font-weight: var(--weight-regular);
  line-height: var(--leading-normal);
}

.text-sm {
  /* Captions, secondary descriptions, nav items, button labels */
  font-family: var(--font-sans);
  font-size: var(--text-sm);
  font-weight: var(--weight-regular);
  line-height: var(--leading-normal);
}

.text-xs {
  /* Fine print, legal text, timestamps */
  font-family: var(--font-sans);
  font-size: var(--text-xs);
  font-weight: var(--weight-regular);
  line-height: var(--leading-normal);
}

.text-label {
  /* UI labels — same size family as body-sm, firmer tone */
  font-family: var(--font-sans);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  line-height: var(--leading-normal);
  letter-spacing: var(--tracking-normal);
}
```

### Practical Text Roles

The utilities above are the visual layer.
In practice, they should be consumed through these role decisions:

- `body-lg` maps to `.text-lg`
- `body` maps to `.text-base`
- `body-sm` maps to `.text-sm`
- `caption` maps to `.text-xs`
- `label` maps to `.text-label`

`label` is intentionally separate from `body-sm`.
They share size territory, but not function.

### How to Use: Text Sizes

```html
<!-- Hero subline: larger than standard body -->
<p class="text-lg">Our formula delivers 4,800mg of human-identical ketone bodies.</p>

<!-- Standard body copy: default size (can omit class if base styles are set) -->
<p class="text-base">Your brain needs fuel or it'll enter a warning state.</p>

<!-- Card description: slightly smaller -->
<p class="text-sm">A clinically tested form of magnesium shown to support cognitive function.</p>

<!-- Fine print under a stat or CTA -->
<p class="text-xs">*Based on 648 clinician recommendations on FrontrowMD.</p>
```

### How to Use: Labels

```html
<label class="text-label" for="email">Email address</label>
```

### The Mono Voice Classes

Plex Mono has its own utility classes since it always pairs specific size + uppercase + letterspacing.

```css
.mono-label {
  /* Standard eyebrow / spec label */
  font-family: var(--font-mono);
  font-size: var(--text-sm);
  font-weight: var(--weight-regular);
  text-transform: uppercase;
  letter-spacing: var(--tracking-mono);
}

.mono-caption {
  /* Smaller mono — stat descriptors, metadata, patent numbers */
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  font-weight: var(--weight-regular);
  text-transform: uppercase;
  letter-spacing: var(--tracking-mono);
}
```

### The Stat Number Class

Stat numbers live outside the modular scale (they're too large and context-specific).

```css
.stat-number {
  font-family: var(--font-sans);
  font-size: var(--text-stat);
  font-weight: var(--weight-medium);
  line-height: var(--leading-none);
  letter-spacing: var(--tracking-tight);
}
```

---

## Complete Class Inventory

This is the full list of base typography classes in the theme. Role language should map back to this inventory rather than generating context-specific variants.

| Class | Font | Size Token | Weight | Leading | Tracking | Transforms |
|-------|------|-----------|--------|---------|----------|------------|
| `.heading-display` | serif | `--text-4xl` | light | tight | tight | — |
| `.heading-1` | sans | `--text-3xl` | medium | tight | normal | — |
| `.heading-1--serif` | serif | `--text-3xl` | light | tight | tight | — |
| `.heading-2` | sans | `--text-2xl` | medium | tight | normal | — |
| `.heading-3` | sans | `--text-xl` | medium | snug | normal | — |
| `.heading-4` | sans | `--text-lg` | medium | snug | normal | — |
| `.heading-5` | sans | `--text-base` | medium | snug | wide | — |
| `.text-xl` | sans | `--text-xl` | regular | snug | — | — |
| `.text-lg` | sans | `--text-lg` | regular | normal | — | — |
| `.text-base` | sans | `--text-base` | regular | normal | — | — |
| `.text-sm` | sans | `--text-sm` | regular | normal | — | — |
| `.text-xs` | sans | `--text-xs` | regular | normal | — | — |
| `.text-label` | sans | `--text-sm` | medium | normal | — | — |
| `.mono-label` | mono | `--text-sm` | regular | — | mono | uppercase |
| `.mono-caption` | mono | `--text-xs` | regular | — | mono | uppercase |

Plus `.stat-number` for display numbers outside the modular scale.

**If a new context needs a heading or text role, pick from this inventory first. Do not create a new context-specific class.** If none fit, the design needs to adjust to the system or the spec needs an intentional update.

---

## Line Heights

```css
:root {
  --leading-none: 1;         /* Display type, stat numbers */
  --leading-tight: 1.15;     /* Headlines */
  --leading-snug: 1.3;       /* Subheadlines, large text */
  --leading-normal: 1.55;    /* Body copy */
  --leading-relaxed: 1.7;    /* Long-form reading (blog posts, article pages) */
}
```

---

## Font Weights

```css
:root {
  --weight-light: 300;       /* Serif headlines (Plex Serif Light) */
  --weight-regular: 400;     /* Body copy, mono labels */
  --weight-medium: 500;      /* Headings, UI labels, subheads, nav items */
  --weight-semibold: 600;    /* Inline emphasis, strong text */
}
```

No bold (700) is used anywhere in the theme. The heaviest weight is Semi-bold (600), and even that is used sparingly — for inline `<strong>` tags within body copy, never for standalone headings.

---

## Letter Spacing

```css
:root {
  --tracking-tight: -0.02em;   /* Large serif headlines — optically tighten at display size */
  --tracking-normal: 0;         /* Body copy, sans-serif at reading sizes */
  --tracking-wide: 0.05em;     /* Smallest headings, slight openness */
  --tracking-mono: 0.1em;      /* Mono labels — always letterspaced */
  --tracking-caps: 0.12em;     /* Uppercase sans-serif labels (rare) */
}
```

---

## Measure (Line Length)

```css
:root {
  --measure: 65ch;             /* Maximum line length for body text */
  --measure-narrow: 45ch;      /* Narrow column text (centered manifesto blocks) */
  --measure-wide: 80ch;        /* Wide column text (only when paired with adjacent content) */
}
```

Body text must never exceed `--measure`. On wide viewports, the grid constrains text columns so this happens naturally. On narrow viewports, the padding handles it.

---

## Typographic Patterns

### The Eyebrow → Headline → Body Stack

The most common typographic pattern on the site. A mono eyebrow sets the context, a serif or sans headline makes the claim, and an Inter body sentence provides the supporting detail.

```html
<span class="mono-label">CLINICALLY STUDIED · PATENTED FORMULA</span>
<h2 class="heading-1--serif">Your brain's preferred fuel</h2>
<p class="text-lg">Our formula delivers 4,800mg of human-identical ketone bodies
directly to your brain — no fasting or keto diet required.</p>
```

### The Stat Block

A large number with a mono descriptor. Used in stat strips and proof sections.

```html
<span class="stat-number">4,800mg</span>
<span class="mono-caption">D-BHB PER SERVING</span>
```

### The Spec List

A vertical list of uppercase mono labels separated by thin horizontal rules. Used for ingredient manifests and feature specs.

```html
<span class="mono-label">D-BHB KETONE BODIES</span>
<hr>
<span class="mono-label">MAGNESIUM BISGLYCINATE</span>
<hr>
<span class="mono-label">B-COMPLEX VITAMINS</span>
```

### Heading in a Tight Context

When a section headline needs to be smaller than its default (e.g., an h2 inside a card or a narrow column):

```html
<!-- Full-width section: h2 at its normal large size -->
<h2 class="heading-1">What's Inside?</h2>

<!-- Same semantic level, but inside a card: h2 at heading-3 size -->
<h2 class="heading-3">Key Ingredients</h2>

<!-- Inside a sidebar or footer: h2 at heading-5 size -->
<h2 class="heading-5">Quick Links</h2>
```

---

## Font Loading Strategy

All three families are Google Fonts / open source and can be self-hosted for performance.

1. Self-host font files in `assets/` as WOFF2.
2. Use `font-display: swap` to prevent FOIT (flash of invisible text).
3. Preload the most critical weights:
   - Inter Regular (400) and Medium (500)
   - IBM Plex Serif Light (300)
   - IBM Plex Mono Regular (400)
4. Load additional weights (Inter Semi-bold 600) as secondary resources.

```html
<link rel="preload" href="{{ 'inter-regular.woff2' | asset_url }}" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="{{ 'ibm-plex-serif-light.woff2' | asset_url }}" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="{{ 'ibm-plex-mono-regular.woff2' | asset_url }}" as="font" type="font/woff2" crossorigin>
```

---

## Rules

1. **Three fonts, three roles.** Never use Plex Serif for body. Never use Plex Mono for headlines. Never use Inter for eyebrows.
2. **No bold (700).** Semi-bold (600) is the maximum weight, used only for inline `<strong>`.
3. **Plex Mono is always uppercase, always letterspaced.** If it's not uppercase and letterspaced, it shouldn't be Plex Mono.
4. **Plex Serif is used sparingly.** One hero headline and 1–2 section headlines per page via `.heading-display` or `.heading-1--serif`.
5. **Body text never exceeds `--measure` (65ch).** The grid enforces this.
6. **Stat numbers use Inter, not Plex Serif.** Stats need to feel precise and modern, not editorial.
7. **No decorative type treatments.** No text shadows, no gradient text, no outlined text, no animated text. The type stands on its own.
8. **Semantic HTML is independent of visual size.** Use the heading/text classes to control appearance. An `<h2 class="heading-4">` is valid and expected.
9. **14 typography classes total.** If the existing classes don't fit a new context, the design adjusts to the system — the system does not grow to accommodate one-off requests.
10. **No context-specific heading classes.** Never create `.hero-h2`, `.card-title`, `.sidebar-heading`, or similar. Use the two-axis system: semantic element + visual class.
