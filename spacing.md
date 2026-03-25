# Lattice — Spacing

## Design Intent

Spacing in Lattice is not a miscellaneous set of token values. It is a governed spatial system with the same level of rigor as the typography system.

The goal is not merely to make spacing fluid. The goal is to make different categories of space behave intelligently:

- tiny optical adjustments stay fixed
- component internals scale gently
- page-level layout spacing expands dramatically

This is what allows the interface to feel precise at the micro level and cinematic at the macro level.

Swiss minimalism depends on this distinction. If every space scales the same way, the system becomes mathematically neat but compositionally blunt. Lattice's spacing system is designed to avoid that trap.

---

## The Spatial Model

The spacing system is built from three behavioral layers:

1. **Optical Layer** — fixed micro-spacing for perceptual precision
2. **Component Layer** — elastic spacing for internal UI rhythm
3. **Layout Layer** — expansive spacing for page composition and section breathing room

These layers share the same viewport anchors as the typography system, but they do not all scale the same way.

That is the core sophistication of the model.

---

## Shared Anchor Conditions

Spacing and typography operate from the same viewport range so that the entire system expands coherently.

```css
:root {
  --viewport-min: 20rem;  /* 320px */
  --viewport-max: 90rem;  /* 1440px */
}
```

### Why This Matters

The typography system already establishes a fluid relationship between 320px and 1440px. Spacing should not use unrelated breakpoints or arbitrary jumps if the intent is to create a truly unified responsive system.

This does **not** mean spacing uses the exact same ratio math as type. It means both systems obey the same environmental conditions while using different growth behavior appropriate to their function.

---

## Behavioral Layers

## 1. Optical Layer

The optical layer is fixed. These values do not scale with the viewport.

They are used for:

- icon-to-label gaps
- tight inline spacing
- compact control padding
- eyebrow micro-separation
- stat-label offsets

### Why It Stays Fixed

At very small values, fluid scaling creates more noise than value. A 4px or 8px relationship is usually performing an optical correction, not establishing compositional rhythm. Scaling those values makes small UI feel sloppy.

---

## 2. Component Layer

The component layer scales moderately across the viewport range.

It is used for:

- heading-to-body spacing
- card padding
- form stacks
- button padding
- grid gaps
- list item spacing
- separation between sibling content groups inside a section

### Why It Scales Moderately

Component internals need to open up on larger screens, but not dramatically. If they expand too aggressively, cards, forms, and UI controls start to feel inflated and structurally weak.

The component layer should breathe more on desktop than mobile, but it should remain disciplined.

---

## 3. Layout Layer

The layout layer scales aggressively across the viewport range.

It is used for:

- section vertical padding
- hero spacing
- major editorial separations
- large compositional breaks
- spacious proof and science sections

### Why It Scales Aggressively

Page-level rhythm is where large screens should feel materially different from small screens. A phone should feel dense but calm. A wide desktop should feel open and architectural.

This layer carries that expansion.

---

## Primitive Tokens

These are the raw spacing tokens. They are organized by behavior, not by one flat numeric ladder.

```css
:root {
  /* ═══════════════════════════════════════════════
     OPTICAL LAYER — Fixed micro-spacing
     Used for perceptual correction and tight internals.
     These values do not scale.
     ═══════════════════════════════════════════════ */

  --space-optical-1: 0.25rem;                                     /* 4px  */
  --space-optical-2: 0.5rem;                                      /* 8px  */
  --space-optical-3: 0.75rem;                                     /* 12px */

  /* ═══════════════════════════════════════════════
     COMPONENT LAYER — Elastic internal rhythm
     Moderate scaling across viewport range.
     For stacks, padding, gaps, and contained UI structure.
     ═══════════════════════════════════════════════ */

  --space-component-1: clamp(0.875rem, 0.804rem + 0.357vw, 1.125rem); /* 14 → 18px */
  --space-component-2: clamp(1rem, 0.857rem + 0.714vw, 1.5rem);       /* 16 → 24px */
  --space-component-3: clamp(1.5rem, 1.286rem + 1.071vw, 2.25rem);    /* 24 → 36px */
  --space-component-4: clamp(2rem, 1.714rem + 1.429vw, 3rem);         /* 32 → 48px */

  /* ═══════════════════════════════════════════════
     LAYOUT LAYER — Expansive page rhythm
     Strong scaling across viewport range.
     For sections, hero spacing, and major compositional divisions.
     ═══════════════════════════════════════════════ */

  --space-layout-1: clamp(2rem, 1.714rem + 1.429vw, 3rem);            /* 32 → 48px */
  --space-layout-2: clamp(3rem, 2.143rem + 4.286vw, 6rem);            /* 48 → 96px */
  --space-layout-3: clamp(4rem, 2.857rem + 5.714vw, 8rem);            /* 64 → 128px */
  --space-layout-4: clamp(5rem, 3.571rem + 7.143vw, 10rem);           /* 80 → 160px */
}
```

---

## Why These Layers Use Different Growth

The optical layer does not grow.

The component layer grows moderately:

- `14 → 18px`
- `16 → 24px`
- `24 → 36px`
- `32 → 48px`

The layout layer grows more aggressively:

- `32 → 48px`
- `48 → 96px`
- `64 → 128px`
- `80 → 160px`

This means the site does not merely get "bigger" on larger screens. It becomes more composed.

Small UI remains precise.
Components gain modest room.
Sections gain dramatic air.

That is the intended behavior.

---

## Semantic Tokens

Primitive tokens should rarely be referenced directly in section or component code. The system should expose intent first.

### Stack Tokens

Used for vertical rhythm between related elements in a text or content stack.

```css
:root {
  --spacing-stack-tight: var(--space-component-1);      /* eyebrow → headline */
  --spacing-stack-default: var(--space-component-2);    /* headline → body */
  --spacing-stack-loose: var(--space-component-3);      /* body → CTA or major content group */
}
```

### Cluster Tokens

Used for horizontal or wrapping groups of related items.

```css
:root {
  --spacing-cluster-tight: var(--space-optical-3);      /* icon + label, compact metadata */
  --spacing-cluster-default: var(--space-component-1);  /* button pairs, pills, nav groups */
  --spacing-cluster-loose: var(--space-component-2);    /* broader grouped controls */
}
```

### Inset Tokens

Used for internal padding of contained UI elements.

```css
:root {
  --spacing-inset-compact: var(--space-optical-3);      /* compact tags, small controls */
  --spacing-inset-default: var(--space-component-2);    /* inputs, standard cards */
  --spacing-inset-generous: var(--space-component-3);   /* featured cards, callout panels */
}
```

### Grid and Group Tokens

Used for repeated content structures and grouped content blocks.

```css
:root {
  --spacing-grid-gap: var(--space-component-3);         /* standard repeated-item gap */
  --spacing-group-gap: var(--space-component-4);        /* major internal separation inside a section */
}
```

### Section Tokens

Used for page-level composition.

```css
:root {
  --spacing-section-compact: var(--space-layout-1);     /* trust strips, thin CTA bars */
  --spacing-section-default: var(--space-layout-2);     /* standard section rhythm */
  --spacing-section-generous: var(--space-layout-3);    /* science, editorial moments */
  --spacing-section-hero: var(--space-layout-4);        /* hero and major visual statements */
}
```

---

## Utility Class Vocabulary

The semantic tokens above are the system's intent layer. These classes are the closed implementation vocabulary used in theme code.

## Section Padding Classes

```css
.section-padding-compact {
  padding-block: var(--spacing-section-compact);
}

.section-padding-standard {
  padding-block: var(--spacing-section-default);
}

.section-padding-generous {
  padding-block: var(--spacing-section-generous);
}

.section-padding-hero {
  padding-block: var(--spacing-section-hero);
}
```

## Stack Gap Classes

```css
.stack-gap-tight {
  gap: var(--spacing-stack-tight);
}

.stack-gap-default {
  gap: var(--spacing-stack-default);
}

.stack-gap-loose {
  gap: var(--spacing-stack-loose);
}
```

## Cluster Gap Classes

```css
.cluster-gap-tight {
  gap: var(--spacing-cluster-tight);
}

.cluster-gap-default {
  gap: var(--spacing-cluster-default);
}

.cluster-gap-loose {
  gap: var(--spacing-cluster-loose);
}
```

## Inset Classes

```css
.inset-compact {
  padding: var(--spacing-inset-compact);
}

.inset-default {
  padding: var(--spacing-inset-default);
}

.inset-generous {
  padding: var(--spacing-inset-generous);
}
```

## Group Classes

```css
.grid-gap-default {
  gap: var(--spacing-grid-gap);
}

.group-gap {
  gap: var(--spacing-group-gap);
}
```

---

## Complete Class Inventory

This is the approved spacing utility inventory for the theme. It is intentionally small.

| Class | Semantic Token | Use |
|-------|----------------|-----|
| `.section-padding-compact` | `--spacing-section-compact` | Trust strips, thin CTA bars, tight editorial separators |
| `.section-padding-standard` | `--spacing-section-default` | Default section vertical padding |
| `.section-padding-generous` | `--spacing-section-generous` | Science sections, editorial moments, spacious proof sections |
| `.section-padding-hero` | `--spacing-section-hero` | Hero and major statement sections |
| `.stack-gap-tight` | `--spacing-stack-tight` | Eyebrow → headline, stat → label, small content stacks |
| `.stack-gap-default` | `--spacing-stack-default` | Headline → body, label → control, standard copy stacks |
| `.stack-gap-loose` | `--spacing-stack-loose` | Body → CTA, major content grouping inside a stack |
| `.cluster-gap-tight` | `--spacing-cluster-tight` | Icon + text, compact metadata rows |
| `.cluster-gap-default` | `--spacing-cluster-default` | Button pairs, nav item groups, inline controls |
| `.cluster-gap-loose` | `--spacing-cluster-loose` | Wider horizontal grouped items |
| `.inset-compact` | `--spacing-inset-compact` | Compact controls, tags, small UI containers |
| `.inset-default` | `--spacing-inset-default` | Standard cards, inputs, contained panels |
| `.inset-generous` | `--spacing-inset-generous` | Featured cards, callouts, spacious containers |
| `.grid-gap-default` | `--spacing-grid-gap` | Repeated-item grids |
| `.group-gap` | `--spacing-group-gap` | Major internal section separation |

If a new spacing need appears, map it to an existing spatial role first. Do not introduce a one-off class because the current local composition feels inconvenient.

---

## Composition Patterns

These are the approved ways the semantic spacing system composes in actual sections and components.

## Eyebrow -> Headline -> Body -> CTA

```text
[eyebrow]
  ↕ stack-tight
[headline]
  ↕ stack-default
[body]
  ↕ stack-loose
[CTA]
```

This is the default editorial stack for hero text and major section intros.

---

## Stat Block

```text
[number]
  ↕ optical
[label]
```

Use:

- `--space-optical-2` or `.stack-gap-tight`

Stat relationships should feel optically precise, not compositionally airy.

---

## Card Interior

```text
[card shell: inset-default]
  [heading]
    ↕ stack-tight
  [body]
    ↕ stack-default
  [supporting metadata / CTA]
```

Featured cards may use `inset-generous`, but the internal rhythm should still usually remain in the component layer.

---

## Repeating Grid

```text
[grid container]
  gap: grid-gap-default

[item]
  [internal stack]
```

Grid rhythm should come from the component layer, not the layout layer.

This is a common failure mode in immature systems: using page-scale spacing inside repeating UI. Do not do that.

---

## Section Intro + Content Area

```text
[section wrapper: section-padding-standard]
  [intro block]
    ↕ group-gap
  [content area]
```

This is the default content-section rhythm.

---

## Trust Strip / Press Strip

```text
[section wrapper: section-padding-compact]
  [logo row: cluster-gap-loose]
```

The section is layout-tight, but the horizontal grouping can still breathe.

---

## Hero

```text
[section wrapper: section-padding-hero]
  [hero stack]
```

Hero uses the most expansive layout layer, but the internal text stack still follows stack semantics rather than arbitrary large gaps.

---

## Relationship to Typography

The typography and spacing systems are parallel, not identical.

Typography governs:

- base size
- hierarchy ratio
- fluid interpolation across viewport range

Spacing governs:

- behavioral layer
- growth intensity
- compositional role

Typography answers: "How much larger should this heading become?"

Spacing answers:

- "Should this space scale at all?"
- "Should it scale gently or dramatically?"
- "Is this an optical correction, a component rhythm, or a layout gesture?"

That distinction is the core upgrade from a standard token ladder to a true design-system spacing model.

---

## Practical Usage Examples

### Standard Section

```html
<section class="section-padding-standard">
  ...
</section>
```

### Text Stack

```html
<div class="stack-gap-default">
  <h2 class="heading-2">Clinically studied ingredients</h2>
  <p class="text-base">A focused blend designed to support the brain under metabolic stress.</p>
</div>
```

### Intro Block Followed by Grid

```html
<section class="section-padding-generous">
  <div class="group-gap">
    <div class="stack-gap-loose">
      <span class="mono-label">WHAT'S INSIDE</span>
      <h2 class="heading-1">The formula</h2>
      <p class="text-lg">Every ingredient earns its place.</p>
    </div>

    <div class="grid-gap-default">
      ...
    </div>
  </div>
</section>
```

### Button Pair

```html
<div class="cluster-gap-default">
  <a class="button button--accent" href="/products/example-product">Try It Now</a>
  <a class="button button--secondary" href="/pages/science">Learn the Science</a>
</div>
```

---

## Rules

1. Never use raw pixel spacing values in theme implementation.
2. Prefer semantic spacing tokens over primitive tokens.
3. Use the optical layer only for micro-spacing and tight perceptual corrections.
4. Use the component layer for card internals, form structure, list rhythm, and grid gaps.
5. Use the layout layer for section padding and major compositional breaks only.
6. Do not use layout-layer spacing inside small repeating UI structures.
7. Do not create one-off spacing utilities because a local context feels awkward. Re-evaluate the composition against the approved spatial roles first.
8. If a new spacing context cannot be described as stack, cluster, inset, grid, group, or section, the pattern likely needs design review before implementation.

---

## Strategic Takeaway

Pixels are static.
Flat token scales are better, but still blunt.
Fluid spacing is an improvement, but only when different kinds of space are allowed to behave differently.

Lattice's spacing system is designed to be:

- tokenized
- fluid where appropriate
- fixed where precision matters
- semantic
- compositional

That is the standard the rest of the design system should match.
