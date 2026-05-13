# Lattice — Color System

## Design Intent

Lattice's color system is built to feel restrained, warm, and clinically composed.

It does not rely on a large palette, loud contrast tricks, or decorative color variety. The visual character comes from disciplined surface control, tonal warmth, and selective accent usage. Color should support authority and calm, not compete with the content.

As with typography, spacing, and grid, the goal is not merely to choose attractive values. The goal is to define a governed system that can be reasoned about, adapted, and implemented without drift.

That means the color system must distinguish:

- source-of-truth color representation
- primitive palette families
- semantic UI meaning
- runtime consumption in theme code

---

## Color System Architecture

Lattice's color system operates in four layers:

1. **Perceptual Source Layer** — OKLCH values as the system foundation
2. **Primitive Token Layer** — named palette families and tonal steps
3. **Semantic Token Layer** — UI roles such as surfaces, text, borders, and actions
4. **Runtime Variable Layer** — CSS custom properties consumed by theme code

This is the color equivalent of the spacing system's behavioral layers and the grid system's structural regimes.

Components should consume semantic tokens.
Primitive tokens exist to support system consistency and future remapping.

### The Primitive Layer Is The Reskin Surface

The specific palette documented in this file — Neutral Creams, Warm Stones, Charcoals, a warm peach/amber Product Accent, and the four status families — is an *example implementation* of the architecture, not the system itself. It describes one brand expression: warm, editorial, wellness-coded.

When Lattice is consumed by a different brand, the primitive layer is what changes. The semantic tokens (`--color-bg-page`, `--color-text-primary`, `--color-action-primary-bg`) keep their names and their roles; the primitives they reference get swapped. A clinical-corporate brand might replace creams and stones with cool neutrals and a saturated cobalt-and-scarlet pair. A tech-utility brand might replace them with deep slates and a single high-chroma accent. Components consuming `--color-action-primary-bg` do not change.

This means a brand swap is, in principle, a primitive-layer edit — not a refactor of every component. The example palette below is the warm-editorial reference; treat it as illustrative, not canonical.

---

## Why OKLCH Is the Source of Truth

The system uses OKLCH as its foundational color representation.

### Why

OKLCH is perceptually uniform, which makes it significantly better than hex, RGB, or HSL for a design system intended to behave coherently.

That means:

- tonal steps feel more even
- contrast can be tuned more intentionally
- accent ramps are easier to control
- future theming becomes more predictable

Hex values are easy to copy. They are not easy to reason about.

OKLCH gives the system a real structure:

- **L** = lightness
- **C** = chroma
- **H** = hue

That is far more useful for systematic color design than memorizing hex values.

---

## Primitive Palette Families

The Lattice palette remains deliberately narrow.

There are five primitive families:

1. **Neutral Creams** — page surfaces and light warmth
2. **Warm Stones** — borders, muted surfaces, secondary text support
3. **Charcoals** — primary text and dark surfaces
4. **Product Accent** — warm peach/amber derived from the drink itself
5. **Status Families** — success, warning, error, info

The system is not built around a rainbow. It is built around tonal control.

---

## Primitive Tokens

These are the perceptual source tokens. They are not used directly in components unless there is a very specific implementation need.

```css
:root {
  /* ═══════════════════════════════════════════════
     NEUTRAL CREAMS
     Warm, near-paper surfaces. Low chroma by design.
     ═══════════════════════════════════════════════ */

  --neutral-50:  oklch(0.988 0.006 85);
  --neutral-100: oklch(0.975 0.009 85);
  --neutral-200: oklch(0.948 0.012 84);

  /* ═══════════════════════════════════════════════
     WARM STONES
     For borders, dividers, subtle contrast surfaces,
     placeholders, and secondary content support.
     ═══════════════════════════════════════════════ */

  --stone-100: oklch(0.922 0.012 78);
  --stone-200: oklch(0.875 0.014 78);
  --stone-300: oklch(0.792 0.015 78);
  --stone-400: oklch(0.688 0.014 78);
  --stone-500: oklch(0.556 0.013 78);
  --stone-600: oklch(0.438 0.012 78);

  /* ═══════════════════════════════════════════════
     CHARCOALS
     For primary text and dark surfaces. Warmed slightly
     to avoid sterile black.
     ═══════════════════════════════════════════════ */

  --charcoal-700: oklch(0.322 0.01 75);
  --charcoal-800: oklch(0.262 0.009 75);
  --charcoal-900: oklch(0.205 0.008 75);

  /* ═══════════════════════════════════════════════
     PRODUCT ACCENT
     Warm peach/amber drawn from the product itself.
     Controlled chroma. Used sparingly.
     ═══════════════════════════════════════════════ */

  --accent-100: oklch(0.95 0.03 70);
  --accent-200: oklch(0.89 0.06 68);
  --accent-400: oklch(0.78 0.11 63);
  --accent-500: oklch(0.69 0.13 58);
  --accent-600: oklch(0.61 0.13 56);

  /* ═══════════════════════════════════════════════
     STATUS FAMILIES
     Quiet, mature feedback colors. Never neon.
     ═══════════════════════════════════════════════ */

  --success-500: oklch(0.57 0.08 145);
  --warning-500: oklch(0.7 0.12 75);
  --error-500:   oklch(0.58 0.13 30);
  --info-500:    oklch(0.6 0.06 240);
}
```

---

## Primitive Palette Logic

### Neutral Creams

The creams are intentionally close together in lightness and low in chroma. Their purpose is to create surface rhythm without visibly "coloring" the interface.

### Warm Stones

The stones handle most supporting UI work:

- borders
- rules
- muted surfaces
- placeholders
- secondary text on light backgrounds

They are not decorative grays. They are the quiet structural layer of the UI.

### Charcoals

The charcoals are slightly warm rather than neutral-cool. This avoids the cold, sterile feel that pure black often introduces into health and wellness interfaces.

### Product Accent

The accent family is derived from the product rather than from generic DTC conventions.

It exists to signal conversion and emphasis, not to decorate the page.

### Status Colors

These exist for clarity, not brand expression. They should feel mature and integrated, never like a separate product palette.

---

## Semantic Token Layer

Primitive tokens should not be used directly in theme sections and components. Theme code consumes semantic tokens that describe purpose.

That makes the system much more stable and future-proof.

---

## Surface Tokens

```css
:root {
  --color-bg-page: var(--neutral-100);
  --color-bg-section-alt: var(--neutral-200);
  --color-bg-raised: var(--neutral-50);
  --color-bg-muted: var(--stone-100);
  --color-bg-dark: var(--charcoal-900);
  --color-bg-dark-secondary: var(--charcoal-800);
  --color-bg-accent-subtle: var(--accent-100);
}
```

These define the major surface hierarchy of the site.

The system should create contrast through tonal steps, not through decorative background color variation.

---

## Text Tokens

```css
:root {
  --color-text-primary: var(--charcoal-900);
  --color-text-secondary: var(--stone-500);
  --color-text-tertiary: var(--stone-400);
  --color-text-on-dark: var(--neutral-100);
  --color-text-on-dark-secondary: var(--stone-300);
  --color-text-accent: var(--accent-500);
}
```

Rules:

- primary text should almost always use `--color-text-primary`
- secondary text should carry supporting explanation, metadata, and captions
- accent-colored text is rare and strategic, not routine

---

## Border and Rule Tokens

```css
:root {
  --color-border-default: var(--stone-100);
  --color-border-strong: var(--stone-200);
  --color-border-dark: var(--charcoal-700);
  --color-rule-default: var(--stone-200);
  --color-rule-dark: var(--charcoal-700);
}
```

Borders and rules should almost always stay quiet. They are structural separators, not expressive gestures.

---

## Interactive Tokens

```css
:root {
  --color-action-primary-bg: var(--charcoal-900);
  --color-action-primary-text: var(--neutral-100);
  --color-action-primary-hover: var(--charcoal-700);

  --color-action-secondary-bg: transparent;
  --color-action-secondary-text: var(--charcoal-900);
  --color-action-secondary-border: var(--charcoal-900);
  --color-action-secondary-hover-bg: var(--charcoal-900);
  --color-action-secondary-hover-text: var(--neutral-100);

  --color-action-accent-bg: var(--accent-500);
  --color-action-accent-text: var(--charcoal-900);
  --color-action-accent-hover: var(--accent-600);

  --color-link: var(--charcoal-900);
  --color-link-hover: var(--stone-600);
  --color-link-visited: var(--charcoal-900);
  --color-link-nav: var(--charcoal-900);
  --color-link-nav-hover: var(--stone-600);
  --color-link-nav-current: var(--charcoal-900);
  --color-link-on-dark: var(--neutral-100);
  --color-link-on-dark-hover: var(--stone-300);
  --color-focus-ring: var(--charcoal-900);
  --color-focus-ring-on-dark: var(--neutral-100);

  --color-state-disabled-text: var(--stone-400);
  --color-state-disabled-border: var(--stone-100);
  --color-state-disabled-surface: var(--stone-100);

  --color-state-selected-surface: var(--stone-100);
  --color-state-selected-border: var(--stone-200);
  --color-state-selected-text: var(--charcoal-900);

  --color-overlay-scrim: color-mix(in oklab, var(--charcoal-900) 72%, transparent);
  --color-overlay-scrim-soft: color-mix(in oklab, var(--charcoal-900) 48%, transparent);

  --color-selection-bg: var(--accent-200);
  --color-selection-text: var(--charcoal-900);
}
```

The interactive system has three modes:

- **primary** — the default high-confidence action
- **secondary** — an outlined or lower-emphasis companion action
- **accent** — the single strongest conversion action in a context

This keeps interaction color intentional rather than arbitrary.

These tokens also establish the base state layer for:

- disabled UI
- selected UI
- overlays and scrims
- text selection

They also define the semantic link layer for:

- inline links
- standalone links
- navigational links
- inverse links

---

## Status Tokens

```css
:root {
  --color-status-success: var(--success-500);
  --color-status-warning: var(--warning-500);
  --color-status-error: var(--error-500);
  --color-status-info: var(--info-500);
}
```

These should be used for state communication:

- success messages
- warning labels
- error messaging
- informational callouts

They are not accent colors for marketing surfaces.

---

## Surface Rhythm

The site's surface rhythm should be expressed through semantic background tokens, not ad hoc local color choices.

### Preferred Page Cadence

| Surface Type | Token |
|-------------|-------|
| Default page or section surface | `--color-bg-page` |
| Alternating light section | `--color-bg-section-alt` |
| Raised or card-like surface | `--color-bg-raised` |
| Muted informational surface | `--color-bg-muted` |
| Dark dramatic section | `--color-bg-dark` |
| Secondary dark section / footer | `--color-bg-dark-secondary` |

This makes color rhythm a structural system, not a decorative improvisation.

---

## Accent Discipline

The accent family is intentionally constrained.

### What the Accent Does

- primary conversion emphasis
- subtle highlighted backgrounds
- occasional emphasis in a headline or key phrase

### What the Accent Does Not Do

- routine text styling
- multi-color icon systems
- decorative highlights everywhere
- section background decoration at full strength

The accent is not the personality of the brand. It is the controlled moment of warmth and activation inside a largely neutral system.

---

## Accessibility and Contrast Logic

Color choices must be validated through contrast behavior, not only aesthetic preference.

### Minimum Requirements

- body text: WCAG AA 4.5:1 minimum
- large text and UI components: 3:1 minimum
- focus indicators: 3:1 minimum against surrounding colors

### Practical Rules

1. `--color-text-primary` on `--color-bg-page` and `--color-bg-section-alt` must exceed AA comfortably.
2. `--color-text-secondary` must remain readable, not merely subtle.
3. Dark sections must always use `--color-text-on-dark` or `--color-text-on-dark-secondary`.
4. Accent buttons must be validated for contrast with their text color, not assumed safe because they "look strong."
5. Decorative subtlety must never compromise usability.

Contrast is a structural property of the system and should be validated during implementation.

---

## Runtime Consumption Rules

The theme should consume semantic runtime variables, not primitive palette tokens.

### Correct

```css
.button--primary {
  background: var(--color-action-primary-bg);
  color: var(--color-action-primary-text);
}
```

### Incorrect

```css
.button--primary {
  background: var(--charcoal-900);
  color: var(--neutral-100);
}
```

The semantic layer exists so implementation can stay stable even if the primitive palette evolves.

---

## Compatibility Note

If external tooling or handoff artifacts require hex output, hex may be provided as a compatibility format.

It is not the source of truth.

The system should be designed in OKLCH and consumed through semantic CSS variables.

---

## What We Do Not Do

1. No gold as a recurring brand system.
2. No purple or blue marketing accents for primary interface behavior.
3. No multi-color iconography.
4. No arbitrary one-off hex values inside implementation code.
5. No component-level color decisions outside the semantic token system.
6. No using feedback colors as brand decoration.
7. No gradients as core palette logic. If gradients ever exist later, they belong to an effects layer, not the core color system.

---

## Strategic Takeaway

Hex and RGB are representations.
HSL is a useful transitional model.
OKLCH is the correct foundation for a modern, governed design system.

For Lattice, the color system should be:

- perceptual
- tokenized
- semantic
- runtime-variable-driven
- visually restrained

That is how the palette becomes a system rather than a moodboard.
