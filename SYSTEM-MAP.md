# Lattice Design System

## Purpose

This folder contains the Lattice design system — a framework for algorithmically derived, behaviorally governed interface design.

Its purpose is to make design and implementation decisions repeatable, system-bound, and legible across designers, developers, and teams. These documents are not inspiration notes. They are the operating specification for how the interface should look, feel, and behave.

The system is designed to prevent:

- ad hoc visual decisions
- local component styling drift
- page design that ignores the underlying rules
- implementation that bypasses the approved design logic

If a design or implementation decision conflicts with this folder, the decision is wrong unless explicitly approved.

---

## System Map

The design system is organized in two layers:

### 1. Foundations

These define the governing logic of the interface.

- [typography.md](./typography.md)
  Three-voice type system, fluid type scale, semantic/visual decoupling, typographic rules.

- [spacing.md](./spacing.md)
  Behavioral spacing model with optical, component, and layout layers plus semantic spacing roles.

- [grid.md](./grid.md)
  Compositional field model with canvas/content/reading width regimes, allocation archetypes, and layout adaptation logic.

- [colors.md](./colors.md)
  OKLCH-based color architecture with primitive families, semantic UI tokens, and runtime variable logic.

### 2. Applied System

These define how the foundations combine into actual interface structures.

- [prose.md](./prose.md)
  Rich text and long-form content container logic for bare HTML, list behavior, inline links, and reading-measure defaults.

- [components.md](./components.md)
  Component architecture: primitives, structured components, patterns, and system consumption rules.

- [buttons.md](./buttons.md)
  Action primitive system with governed roles and a shared control size axis.

- [forms.md](./forms.md)
  Form primitives and field composition rules aligned to buttons and type roles.

- [badges.md](./badges.md)
  Compact badge and tag primitives for informational labels and filter-like UI.

- [density.md](./density.md)
  Context-level spatial character system for compact, default, and relaxed interface rhythm.

- [surfaces.md](./surfaces.md)
  Structural surface hierarchy for page planes, raised layers, muted callouts, dark sections, and overlay behavior.

- [links.md](./links.md)
  Link families for inline, standalone, navigational, and inverse link behavior.

- [states.md](./states.md)
  Cross-component state logic for disabled, selected, loading, focus, scrims, and text selection.

- [motion.md](./motion.md)
  Motion and interaction rules for feedback, state change, entrances, and performance-safe behavior.

- [section-archetypes.md](./section-archetypes.md)
  Approved reusable section families that translate the design system into actual page-building grammar.

---

## Reading Order by Role

### Designers

Read in this order:

1. [typography.md](./typography.md)
2. [spacing.md](./spacing.md)
3. [grid.md](./grid.md)
4. [colors.md](./colors.md)
5. [prose.md](./prose.md)
6. [components.md](./components.md)
7. [buttons.md](./buttons.md)
8. [forms.md](./forms.md)
9. [badges.md](./badges.md)
10. [density.md](./density.md)
11. [surfaces.md](./surfaces.md)
12. [links.md](./links.md)
13. [states.md](./states.md)
14. [motion.md](./motion.md)
15. [section-archetypes.md](./section-archetypes.md)

### Developers

Read in this order:

1. [typography.md](./typography.md)
2. [spacing.md](./spacing.md)
3. [grid.md](./grid.md)
4. [colors.md](./colors.md)
5. [prose.md](./prose.md)
6. [components.md](./components.md)
7. [buttons.md](./buttons.md)
8. [forms.md](./forms.md)
9. [badges.md](./badges.md)
10. [density.md](./density.md)
11. [surfaces.md](./surfaces.md)
12. [links.md](./links.md)
13. [states.md](./states.md)
14. [motion.md](./motion.md)
15. [section-archetypes.md](./section-archetypes.md)

### Strategists / Content

Read in this order:

1. [colors.md](./colors.md)
2. [typography.md](./typography.md)
3. [prose.md](./prose.md)
4. [buttons.md](./buttons.md)
5. [density.md](./density.md)
6. [surfaces.md](./surfaces.md)
7. [links.md](./links.md)
8. [states.md](./states.md)
9. [section-archetypes.md](./section-archetypes.md)

### QA / Accessibility

Read in this order:

1. [typography.md](./typography.md)
2. [spacing.md](./spacing.md)
3. [grid.md](./grid.md)
4. [colors.md](./colors.md)
5. [prose.md](./prose.md)
6. [components.md](./components.md)
7. [buttons.md](./buttons.md)
8. [forms.md](./forms.md)
9. [badges.md](./badges.md)
10. [density.md](./density.md)
11. [surfaces.md](./surfaces.md)
12. [links.md](./links.md)
13. [states.md](./states.md)
14. [motion.md](./motion.md)
15. [section-archetypes.md](./section-archetypes.md)

---

## Dependency Logic

The files are not equal peers. They depend on each other in a specific way.

### Foundation Dependency Order

1. Typography defines hierarchy and readable scale.
2. Spacing defines spatial behavior and rhythm.
3. Grid defines occupancy, containment, and compositional allocation.
4. Color defines surface hierarchy, text contrast, and action meaning.

These four files define the underlying language of the interface.

### Applied Dependency Order

5. Prose maps the foundations onto real authored content.
6. Components inherit from typography, spacing, grid, and color.
7. Buttons define the primary action primitive and shared control size model.
8. Forms and badges inherit that primitive logic for everyday UI use.
9. Density defines the spatial character contexts use when consuming the spacing system.
10. Surfaces define the interface planes those components and sections occupy.
11. Links define the text-level interaction families that sit between prose and buttons.
12. States define cross-component interaction behavior and availability logic.
13. Motion governs how those structures respond and transition.
14. Section archetypes combine all of the above into reusable page-building units.

This means:

- prose should not invent its own type scale or spacing logic
- components should not invent their own private spacing or color system
- density should not be adjusted through arbitrary local spacing overrides
- surfaces should not be chosen ad hoc at the section or component level
- states should not be redefined locally inside every primitive
- motion should not contradict component or layout logic
- section archetypes should not bypass the foundations

---

## Rules of Use

1. Do not create local tokens when a system token already exists.
2. Do not build new sections before identifying the correct archetype.
3. Do not design pages from blank canvases when an approved archetype already fits.
4. Do not style components directly from primitive color tokens when semantic tokens exist.
5. Do not introduce ad hoc spacing rules inside components or sections.
6. Do not bypass the prose container for merchant-authored rich text.
7. Do not bypass reading measure for long-form copy.
8. Do not create a new archetype unless the existing system genuinely cannot express the need.

---

## What This Folder Does Not Contain

This folder does not define:

- page-by-page final compositions
- merchant content strategy
- SEO content hierarchy
- Shopify implementation details
- copywriting

Those are separate layers of work.

This folder defines the design language those layers must obey.
