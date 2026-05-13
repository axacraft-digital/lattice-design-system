# Lattice — Surfaces

## Design Intent

Surfaces define where UI lives.

They answer questions such as:

- what is the default page plane
- when should a card feel raised
- when should a section use an alternate surface
- what counts as muted versus dark
- how should overlays sit above the rest of the interface

Without a surface model, teams still have color tokens, but they do not have a compositional hierarchy.
That leads to local background choices, inconsistent containment, and overuse of dark or accented sections.

Surfaces are not just colors.
They are the structural planes of the system.

---

## Surface Families

Lattice defines six primary surface families:

1. page
2. section-alt
3. raised
4. muted
5. dark
6. accent-subtle

There is also one elevated atmospheric layer:

7. overlay

These are semantic planes, not decorative swatches.

---

## Surface Token Layer

Surface tokens are owned by `colors.md`.
This file defines when and why they should be used.

```css
:root {
  --color-bg-page: var(--neutral-100);
  --color-bg-section-alt: var(--neutral-200);
  --color-bg-raised: var(--neutral-50);
  --color-bg-muted: var(--stone-100);
  --color-bg-dark: var(--charcoal-900);
  --color-bg-dark-secondary: var(--charcoal-800);
  --color-bg-accent-subtle: var(--accent-100);

  --color-overlay-scrim: color-mix(in oklab, var(--charcoal-900) 72%, transparent);
  --color-overlay-scrim-soft: color-mix(in oklab, var(--charcoal-900) 48%, transparent);
}
```

The goal is not to create many surfaces.
The goal is to make a few surfaces behave predictably.

---

## The Base Plane

### Page Surface

`--color-bg-page` is the default resting plane of the interface.

Use it for:

- default sections
- base page background
- uncontained content areas
- most reading environments

Rules:

1. This is the system default.
2. If no stronger surface logic is needed, stay on the page plane.
3. Most interfaces should spend the majority of their time here.

---

## Rhythm Surfaces

### Alternate Section Surface

`--color-bg-section-alt` creates quiet rhythm between adjacent light sections.

Use it for:

- alternating page cadence
- separating adjacent content families without introducing containment
- giving editorial rhythm to long pages

Rules:

1. Use for section-to-section contrast, not component containment.
2. It should feel like a tonal shift, not a different theme.
3. Do not alternate mechanically every single section.

### Muted Surface

`--color-bg-muted` is a quieter contained surface used for informational support.

Use it for:

- notes
- subtle callouts
- filter states
- inline code backgrounds
- low-emphasis supporting boxes

Rules:

1. Muted surfaces are supportive, not dominant.
2. They are quieter than raised surfaces.
3. Do not use muted surfaces for major conversion blocks.

---

## Containment Surfaces

### Raised Surface

`--color-bg-raised` is for components that need containment without shadow language.

Use it for:

- cards
- drawers
- floating panels
- contained form groups
- light modals layered over the page

Rules:

1. Raised does not mean shadow-heavy.
2. Raised surfaces rely on edge, contrast, and spacing more than effects.
3. Use raised surfaces when containment improves comprehension, not by default.

### Accent-Subtle Surface

`--color-bg-accent-subtle` is a warm highlight plane.

Use it for:

- gentle product emphasis
- small promotional callouts
- key proof moments that need a slight lift

Rules:

1. Accent-subtle is rare.
2. It should warm the interface, not brand-wash it.
3. Never treat it like a default section background.

---

## Dark Surfaces

### Dark Primary

`--color-bg-dark` is the dramatic plane.

Use it for:

- hero surfaces
- strong proof sections
- mechanism or science moments with more theatrical contrast
- footer or closing conversion environments when warranted

### Dark Secondary

`--color-bg-dark-secondary` is a supporting dark plane.

Use it for:

- footer interiors
- nested dark containers
- secondary dark groupings inside a larger dark context

Rules:

1. Dark surfaces are strategic, not default.
2. They should punctuate the page, not dominate it.
3. Any dark surface must switch text, border, and link behavior to the dark-surface token family.
4. If multiple dark sections appear on the same page, each one must earn it.

---

## Overlay Surfaces

Overlay surfaces sit above the page hierarchy.

Use them for:

- modal scrims
- drawer backdrops
- temporary attention management

Rules:

1. Overlay is not a content surface.
2. It controls separation and attention, not narrative rhythm.
3. Use `--color-overlay-scrim` and `--color-overlay-scrim-soft` from the state layer.

---

## Stacking Order

The surface model determines what each plane *is*. The stacking-order model determines how those planes layer when they overlap.

A governed z-index scale prevents the most common drift in any growing interface: every contributor reaching for an arbitrary `z-50`, `z-99`, or `z-9999` until the layering becomes a guessing game.

### The Scale

```css
:root {
  --z-base:      0;     /* default page content */
  --z-raised:    10;    /* cards or content lifted from the page on hover */
  --z-sticky:    20;    /* sticky section headers, sticky form labels */
  --z-nav:       30;    /* site header */
  --z-dropdown:  40;    /* mega-menus, services dropdowns, command palette */
  --z-overlay:   50;    /* mobile nav drawer, side sheets, scrims */
  --z-modal:     60;    /* dialog modals */
  --z-toast:     70;    /* toast / snackbar notifications */
  --z-popover:   80;    /* tooltips, popovers, hover help */
  --z-debug:     9999;  /* reserved for dev overlays — never ships */
}
```

### Why Popover Sits Above Modal

The most counterintuitive line in the scale is that `--z-popover` sits *above* `--z-modal`. This is intentional.

Tooltips and popovers exist to provide contextual help. If a modal contains a form with a complex field, the tooltip explaining that field must be reachable. Putting popover below modal would either make the help invisible or force the user to dismiss the modal to read it. The latter is worse — they lose their work to learn how to do it.

Toasts sit between modal and popover for the same reason: a confirmation that fires from inside a modal should still be visible.

### Rules of Use

1. **Never invent an arbitrary z-value.** No `z-index: 999`. No `z-50` Tailwind utility chosen because it "looks high enough." Every stacked element consumes a token from the scale above.
2. **One token per stacking role.** Do not introduce a new token unless the existing scale genuinely cannot express the relationship. If a new role appears, document it in the same change that introduces it.
3. **Stacking is a system decision, not a component decision.** A component author should not need to know the absolute z-index value of any other component. They consume the role token and trust the scale.
4. **Debug overlays use `--z-debug` and never ship.** This is a development-only surface. Production builds should fail to build (or visibly warn) if a `--z-debug` value reaches the deployed bundle.

### What Does Not Belong On The Scale

Decorative effects (drop shadows, glows, blurred backgrounds) are a *visual* layer, not a *stacking* layer. They should be expressed through surface tokens, color tokens, or component-level styling — never through a z-index escalation.

If a contributor reaches for z-index to make something "feel more important," that is a signal to fix the surface, contrast, or composition — not to push the element up the stack.

---

## Surface Pairing Rules

Every surface implies companion tokens.

### On Light Surfaces

Use:

- `--color-text-primary`
- `--color-text-secondary`
- `--color-border-default`
- standard link tokens

### On Dark Surfaces

Use:

- `--color-text-on-dark`
- `--color-text-on-dark-secondary`
- `--color-border-dark`
- inverse link tokens
- dark-surface focus ring token

Rules:

1. Changing the surface changes the companion text and interaction layer.
2. Dark surfaces are not just a background swap.
3. Raised and muted surfaces usually stay in the light-surface text family unless explicitly nested in dark contexts.

---

## Surface Hierarchy In Components

Components should consume surfaces in this order:

1. Can this remain on the page plane
2. Does it need quiet rhythmic distinction
3. Does it need containment
4. Does it need emphasis
5. Does it need dramatic contrast

This prevents over-boxing and over-highlighting.

Examples:

- a simple testimonial list may stay on `page`
- a grouped testimonial card may use `raised`
- a technical note may use `muted`
- a hero may use `dark`
- a small highlighted message may use `accent-subtle`

---

## Section Usage Rules

1. Default sections should prefer `page`.
2. Adjacent sections may use `section-alt` when tonal rhythm improves legibility.
3. Dark surfaces should be reserved for emphasis, not used as routine alternation.
4. Accent-subtle should be used sparingly and locally.
5. Full-bleed is a grid/frame decision. Surface choice is a color/plane decision. They are related but not identical.

---

## What We Do Not Do

1. No arbitrary one-off background colors for individual sections.
2. No using dark surfaces simply to “make it pop.”
3. No stacking multiple competing contained surfaces without clear hierarchy.
4. No treating raised surfaces as a license for shadows and ornamental effects.
5. No using accent backgrounds at full strength as routine section rhythm.

---

## Recommended API

```css
.surface-page {
  background: var(--color-bg-page);
}

.surface-alt {
  background: var(--color-bg-section-alt);
}

.surface-raised {
  background: var(--color-bg-raised);
}

.surface-muted {
  background: var(--color-bg-muted);
}

.surface-dark {
  background: var(--color-bg-dark);
  color: var(--color-text-on-dark);
}

.surface-accent-subtle {
  background: var(--color-bg-accent-subtle);
}
```

These are not mandatory class names, but they represent the intended closed vocabulary.

---

## Strategic Takeaway

Color tokens tell you what colors exist.
Surfaces tell you how the interface is layered.

That distinction is what keeps a design system from becoming a bag of nice backgrounds.
