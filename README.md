# Lattice

Lattice is a design system built around derivation instead of selection.

Instead of treating design as a series of isolated choices like picking font sizes, spacing values, button styles, and section layouts one by one, Lattice defines the logic that governs those decisions so interfaces stay coherent as they evolve.

It is designed for teams who want design and implementation to stay structurally aligned, not drift apart.

## Core Idea

Most design systems document outputs.

Lattice starts by documenting the rules that produce those outputs.

That means:

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
10. `density.md`
11. `surfaces.md`
12. `links.md`
13. `states.md`
14. `motion.md`
15. `section-archetypes.md`

## Current Status

Lattice is currently documentation-first.

It defines the design logic, system layers, primitives, and archetypes needed to implement a coherent interface system across design and development.

A coded implementation layer may follow, but the documentation is the source of truth.

## Philosophy

Typical design asks:

"What looks right here?"

Lattice asks:

"What system can produce the right answer here, and keep producing it as the interface changes?"

## License

No license has been declared yet.
