# Lattice

Lattice is a design system built around responsive logic instead of fixed screen assumptions.

Rather than designing for a few breakpoints, it defines how typography, spacing, layout, color, and section composition should behave across the full spectrum of real device sizes.

The goal is to make websites feel intentionally composed at 320px, 1440px, and everywhere between — without relying on ad hoc adjustments or one-off responsive fixes.

## Core Idea

Typical responsive design starts with a few target breakpoints — mobile, tablet, desktop. Designers make layouts for those widths, then developers fill the gaps with media queries, overrides, and one-off adjustments.

Lattice starts from behavior instead. It defines the rules that produce coherent output at any width:

- typography is derived from a governed fluid scale
- spacing is separated by behavior, not flattened into one ladder
- layout responds to composition, not only breakpoints
- color is defined semantically from a perceptual source model
- components consume the system instead of inventing local rules
- sections are composed from archetypes instead of blank-canvas improvisation

## What's In This Repository

### Foundations

- `typography.md`
- `spacing.md`
- `grid.md`
- `colors.md`

### Consumption Layers

- `prose.md`
- `density.md`
- `surfaces.md`
- `links.md`
- `states.md`

### Components

- `components.md`
- `buttons.md`
- `forms.md`
- `badges.md`
- `icons.md`

### Composition

- `motion.md`
- `section-archetypes.md`

The full internal system map and dependency guide lives in [`SYSTEM-MAP.md`](./SYSTEM-MAP.md).

## Who This Is For

Lattice is for:

- designers who want systems to be operational, not inspirational
- developers who want clearer implementation rules
- teams tired of local UI drift
- people building editorial, commerce, product, or brand interfaces that need structural consistency

## What Makes Lattice Different

Lattice is not:

- a UI kit
- a component library
- a token dump
- a moodboard
- a set of nice defaults

It is a governed interface system.

Its purpose is to reduce arbitrary decisions by defining the grammar behind interface construction.

## Reading Order

If you're new to the system, read in this order:

1. `typography.md`
2. `spacing.md`
3. `grid.md`
4. `colors.md`
5. `prose.md`
6. `components.md`
7. `buttons.md`
8. `forms.md`
9. `badges.md`
10. `icons.md`
11. `density.md`
12. `surfaces.md`
13. `links.md`
14. `states.md`
15. `motion.md`
16. `section-archetypes.md`

## Current Status

Lattice is currently documentation-first.

It defines the design logic, system layers, primitives, and archetypes needed to implement a coherent interface system across design and development.

A coded implementation layer may follow, but the documentation is the source of truth.

## Philosophy

Typical responsive design asks:

"What should this look like at desktop?"

Lattice asks:

"How should this relationship behave as the viewport changes?"

## License

Lattice is released under the [MIT License](./LICENSE) — free to use, adapt, and build on, including commercially.
