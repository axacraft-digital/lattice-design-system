# Lattice — Component System

## Design Intent

Lattice's component system exists to translate the design foundations into repeatable interface behavior.

It should not read like a grab bag of styled widgets. It should read like a governed component architecture built from the systems already defined in:

- typography
- spacing
- grid
- color
- density
- surfaces
- links
- states

That means components are not authored from isolated visual decisions. They are assembled from shared primitives:

- semantic type roles
- semantic spacing roles
- frame and allocation behavior
- semantic color tokens
- context-level density choices
- approved surface planes
- role-based link behavior
- cross-component state rules

The result should feel restrained, precise, and structurally calm.

---

## Component System Architecture

The component system operates in three layers:

1. **Primitives** — low-level reusable UI parts such as buttons, inputs, rules, icons
2. **Structured Components** — self-contained content units such as cards, stat blocks, testimonials
3. **Patterns** — recurring compositional arrangements such as trust strips, spec lists, and navigation

This distinction matters.

A button is not the same kind of object as a testimonial block.
A testimonial block is not the same kind of object as a navigation system.

The old failure mode of component docs is flattening everything into a single catalog. Lattice's component system should avoid that.

---

## What Components Consume

Components must be authored from the semantic layers of the design system.

### Typography

Use:

- heading classes
- text classes
- mono-label classes
- stat number classes

Do not invent local type hierarchies inside components.

### Spacing

Use:

- stack tokens for vertical rhythm
- cluster tokens for horizontal groups
- inset tokens for internal padding
- group and grid tokens for repeated content structures

Do not reach for one-off numeric spacing decisions.

### Grid

Use:

- frame modes
- reading width when sustained prose appears
- allocation archetypes only when the component itself spans multiple regions

Not every component needs grid logic, but every larger pattern must respect the grid system.

### Color

Use:

- semantic action tokens
- semantic surface tokens
- semantic text tokens
- semantic border and rule tokens

Do not style components with primitive palette tokens unless the semantic layer explicitly calls for it.

### Density

Use:

- `compact`, `default`, or `relaxed` as context-level rhythm decisions
- density to choose between tighter or looser stack, cluster, and inset behavior
- density to determine whether controls should lean `sm`, `md`, or `lg`

Do not solve component rhythm with local spacing exceptions when density is the real decision.

### Surfaces

Use:

- page surface for default resting contexts
- raised surface for containment
- muted surface for supportive callouts
- dark surface only when stronger contrast is structurally justified

Do not choose backgrounds ad hoc at the component level.

### Links

Use:

- inline links for prose-like text environments
- standalone links for low-emphasis adjacent actions
- nav links only in structural navigation contexts
- inverse links when the component sits on a dark surface

Do not style every anchor as if it were the same object.

### States

Use:

- shared focus-visible behavior
- shared disabled logic
- shared selected logic
- shared loading behavior
- shared overlay behavior where relevant

Do not redefine state semantics inside each component file.

---

## Primitive Components

These are the smallest repeatable building blocks.

### Primitive Files

- [buttons.md](./buttons.md)
  Action primitives with a governed role axis and shared `sm / md / lg` size axis.

- [forms.md](./forms.md)
  Inputs, labels, help text, error text, and field composition rules aligned to the same control sizing model as buttons.

- [badges.md](./badges.md)
  Compact informational and interactive label primitives for tags, pills, and status markers.

- [links.md](./links.md)
  Text-level interaction families for inline, standalone, navigational, and inverse links.

- [density.md](./density.md)
  Context-level rhythm tuning for compact, default, and relaxed component usage.

- [surfaces.md](./surfaces.md)
  Structural surface hierarchy that determines the planes components occupy.

- [states.md](./states.md)
  Cross-component behavior for focus, disabled, selected, loading, and overlay logic.

The component file is now the system map for primitives, structured components, and patterns.
Practical primitive rules live in their own documents so teams can find them immediately.

---

## Icons

Icons are scanability tools, not illustration systems.

### Library

Lucide is the default icon language for the theme.

### Icon Logic

```text
Stroke:        Lucide default
Fill:          none
Color:         currentColor
Role:          supporting, not dominant
```

### Icon Scale

```css
:root {
  --icon-sm: 1rem;     /* 16px */
  --icon-md: 1.5rem;   /* 24px */
  --icon-lg: 2.5rem;   /* 40px */
}
```

### Icon Rules

1. Icons inherit semantic text color through `currentColor`.
2. No decorative icon containers.
3. No multi-color icon treatments.
4. If the text already communicates the idea clearly, the icon should be omitted rather than repeated redundantly.
5. Custom icons must visually match the Lucide system.

---

## Horizontal Rules

Rules are structural separators. They belong to the border system, not the accent system.

### Rule Logic

```text
Color:         --color-rule-default
Dark variant:  --color-rule-dark
Width:         content field only
Spacing:       component-to-group separation, not page-scale spacing
```

Recommended mapping:

```css
:root {
  --component-rule-spacing: var(--spacing-group-gap);
}
```

### Rule Rules

1. Use rules to separate repeated content rows, feature descriptions, FAQ items, or spec lines.
2. Rules should never become decorative motifs.
3. Rules align to the content field, not the viewport.

---

### Primitive Rules

1. Primitives should share a coherent size axis where alignment matters.
2. Buttons, inputs, and inline controls must feel like members of one system family.
3. Compact primitives such as tags and badges should not drift into miniature button design.
4. Primitive files define defaults so practitioners do not invent them locally.
5. Primitive behavior should resolve through the shared state layer before introducing local exceptions.
6. Primitive rhythm should follow density decisions before adding bespoke spacing.

---

## Structured Components

These are self-contained content units that combine primitives, typography, spacing, and surface behavior.

## Cards

Cards are optional containment devices, not the default answer to repetition.

Many Lattice layouts should prefer list/grid structures with rules over boxed cards. Cards are used only when containment materially improves clarity.

### Card Logic

Cards consume:

- a semantic surface token
- border tokens
- inset tokens
- stack spacing roles
- a density choice

```text
Surface:       --color-bg-page, --color-bg-section-alt, or --color-bg-raised
Border:        --color-border-default
Padding:       inset-default or inset-generous
Geometry:      square corners
Shadow:        none
```

Default component posture:

- density: `default`
- surface: `raised` only when containment is necessary
- states: hover may strengthen border only
- links: supporting actions prefer `link-standalone` before button usage

### Card Interior Model

```text
[optional media or icon]
  ↕ stack-default
[heading]
  ↕ stack-tight
[body]
  ↕ stack-default
[supporting metadata / action]
```

### Card Rules

1. Cards are defined by edge, spacing, and typography, not shadow.
2. Cards do not introduce local color logic beyond semantic surface choices.
3. Clickable cards may shift border strength on hover; they do not lift, scale, or shadow.
4. If the content works better as a ruled list or open grid, do that instead of forcing a card.
5. Compact cards should change density first, not invent tighter local spacing tokens.

---

## Stat Block

A stat block is a structured evidence component built from the typography system.

### Stat Block Logic

```text
[number]   stat-number class + semantic text color
  ↕ stack-tight or optical separation
[label]    mono-label class + secondary text role
```

The number is the dominant signal.
The descriptor is quiet and technical.

Default component posture:

- density: `compact`
- surface: page or dark, depending on the proof band context
- links: none by default
- states: no animated count-up behavior

### Stat Block Rules

1. No animated counters.
2. The label should be short, uppercase, and mono.
3. Stat groups may use balanced distribution or simple rules, but not decorative framing.

---

## Testimonial

A testimonial is a content unit, not a slider module.

### Testimonial Logic

Testimonials consume:

- text hierarchy
- stack spacing
- reading measure when the quote is long
- optional containment only when needed
- a default density choice

```text
[quote text]   text-lg or text-base depending on context
  ↕ stack-default
[name]         text-sm, medium
[context]      mono-label role, secondary text
```

Default component posture:

- density: `default`
- surface: page by default, raised only when grouping materially helps
- links: supporting proof exploration should use `link-standalone`
- states: no carousel-specific state model by default

### Testimonial Rules

1. No decorative quote marks as visual ornaments.
2. No carousel by default.
3. Long quotes should respect reading measure.
4. Use a static grid or open list before considering any more complex presentation.

---

## Component Patterns

These are recurring compositions built from primitives and structured components.

## Trust Strip / Press Row

This is a pattern, not a primitive component.

### Pattern Logic

```text
Frame:         full span within a contained section
Spacing:       cluster-based horizontal spacing
Color:         monochrome / inherited semantic text color
Surface:       usually default page surface
```

### Pattern Rules

1. Logos are monochrome.
2. Logo height is controlled; width may vary.
3. Use cluster spacing semantics instead of custom logo gaps.
4. If there are too many logos, simplify the set rather than turning it into a noisy scroller unless the design explicitly supports it.

---

## Spec List

The spec list is a repeated structured pattern built from mono labels, optional icons, and rules.

### Pattern Logic

```text
[optional icon]  [mono label]
────────────────────────
[optional icon]  [mono label]
```

It should feel technical and orderly, not decorative.

### Pattern Rules

1. The icon is optional.
2. The row spacing should use cluster logic.
3. The separation between rows should use rules plus stack/group logic.
4. This pattern is ideal for ingredients, proof labels, certifications, and feature breakdowns.

---

## Navigation

Navigation is a high-level pattern, not a primitive.

It should be described through structure and behavior, not just appearance.

### Navigation Logic

```text
[brand mark / logo]   [nav group]   [primary action]
```

Consumes:

- cluster spacing for horizontal grouping
- semantic action styles for the CTA
- transparent-to-solid surface behavior as defined in motion
- simple frame logic from the grid system
- nav link family from `links.md`
- density guidance from `density.md`

### Navigation Rules

1. Maximum five primary nav items plus one action.
2. No mega-menu system by default.
3. Mobile navigation should become a coherent full-screen or full-panel pattern, not a cramped dropdown.
4. Navigation should remain structurally simple enough to preserve the brand's calm tone.
5. Navigation links use the nav-link family, not standalone or inline link behavior.
6. Navigation interiors are usually `compact` density even when the page body is not.

---

## Decision Rules

When designing or implementing a component, choose in this order:

1. Is this a primitive, a structured component, or a pattern?
2. What density should this context use: compact, default, or relaxed?
3. What surface plane should it occupy: page, raised, muted, dark, or accent-subtle?
4. What semantic color roles does it need?
5. What spacing roles does it consume: stack, cluster, inset, group?
6. Does it need inline links, standalone links, nav links, or no links at all?
7. What shared states should it support?
8. Does it need content width, reading width, or a larger frame?
9. Is containment actually necessary, or is the component stronger when left open?

This prevents local component decisions from drifting away from the governing system.

---

## What We Do Not Build

1. No decorative shadows as a primary component language.
2. No rounded-corner aesthetic as a default system move.
3. No icon badges, colored icon circles, or ornamental icon containers.
4. No testimonial carousels by default.
5. No floating or sticky conversion widgets that break the page rhythm.
6. No modal email capture on entry.
7. No component-local color decisions that bypass the semantic token layer.
8. No one-off spacing logic inside components when semantic spacing roles already exist.
9. No local density hacks when the context should simply be compact or relaxed.
10. No ad hoc surface treatments outside the approved surface hierarchy.
11. No component-specific link styles that bypass the link families.
12. No local reinvention of disabled, selected, loading, or focus logic.

---

## Strategic Takeaway

A legacy component file tells you what each widget looks like.

A mature component system tells you:

- what kind of object something is
- what system layers it consumes
- how it behaves structurally
- when it should or should not exist as a contained component

That is the standard Lattice's component system should meet.
