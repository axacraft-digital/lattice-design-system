# Lattice — Density

## Design Intent

Density controls the spatial character of the interface.

It answers questions such as:

- should this UI feel compact or open
- how tightly should controls sit together
- when should a section feel editorial versus operational
- how can teams tune rhythm without inventing local spacing overrides

Without a density model, practitioners start making one-off adjustments:

- a tighter card here
- a looser filter row there
- a custom small form stack somewhere else

That is spacing drift disguised as pragmatism.

Density is not a replacement for the spacing system.
It is a consumption layer that tells the spacing system how tightly a context should feel.

---

## Density Modes

Lattice defines three density modes:

1. compact
2. default
3. relaxed

These are controlled context modes, not unlimited stylistic choices.

### Compact

Use when the interface needs to feel efficient, structured, and operational.

Typical contexts:

- filter bars
- product metadata
- compact cards
- navigation interiors
- tool-like UI clusters

### Default

The system baseline.

Use for:

- most page content
- standard forms
- standard cards
- regular section internals

### Relaxed

Use when the interface should feel editorial, generous, or premium.

Typical contexts:

- manifesto sections
- hero-adjacent content
- founder story modules
- spacious proof layouts
- elevated callout groups

---

## What Density Changes

Density does not rewrite the whole system.
It adjusts specific spatial relationships:

- stack rhythm
- cluster spacing
- inset behavior
- control sizing tendencies
- local group spacing

Density should not arbitrarily change:

- color roles
- type scale
- grid regime
- component taxonomy

It is a rhythm modifier, not a redesign switch.

---

## Density Mapping

Density modes should map to existing spacing semantics rather than inventing new raw values.

### Compact

```text
stack:     tight → default
cluster:   tight → default
inset:     compact → default
section:   compact only when the section genuinely needs it
controls:  prefer sm or md
```

### Default

```text
stack:     default
cluster:   default
inset:     default
section:   default
controls:  md
```

### Relaxed

```text
stack:     default → loose
cluster:   default → loose
inset:     default → generous
section:   default → generous
controls:  md or lg depending on context
```

The key rule is that density moves by semantic step, not by custom pixel choice.

---

## Density And Components

Density should influence components in predictable ways.

### Buttons And Controls

- compact density prefers `sm` or `md`
- default density prefers `md`
- relaxed density may use `md` or `lg`

Density does not create extra sizes.
It changes which existing sizes are appropriate.

### Cards

- compact cards use tighter stacks and avoid excessive inset
- default cards use the standard internal rhythm
- relaxed cards may use generous inset and looser internal grouping

### Tags And Badges

- compact density often uses `sm`
- default density uses `md`
- relaxed density rarely enlarges tags; it usually changes surrounding spacing instead

---

## Density And Sections

Density is especially important at section level.

### Compact Sections

Use for:

- trust strips
- dense product comparison areas
- concise proof bars
- utility-heavy layouts

Guidance:

- `section-padding-compact`
- tighter internal grouping
- restrained copy stack

### Default Sections

Use for most of the site.

Guidance:

- `section-padding-default`
- standard stack and group rhythm

### Relaxed Sections

Use for:

- science storytelling
- editorial narrative
- emotional conversion moments
- visually calm educational layouts

Guidance:

- `section-padding-generous`
- looser internal groups
- longer breathing room between major content families

---

## Density And Prose

Density affects how prose is framed around the content, not the reading measure itself.

Rules:

1. Prose stays governed by `prose.md`.
2. Density changes the spacing around prose blocks, not the line length logic.
3. Relaxed density pairs naturally with `.prose-lg` or generous section rhythm.
4. Compact density may use `.prose-sm` in operational contexts.

---

## Composition Rules

1. Default is the baseline. Do not choose compact or relaxed without reason.
2. Compact should improve efficiency, not create visual starvation.
3. Relaxed should create calm, not empty space for its own sake.
4. A page may combine densities, but transitions should be intentional.
5. Density is chosen at the context level, not per random element.

---

## Recommended API

These are conceptual classes, not mandatory implementation names.

```css
.density-compact {
  --density-stack: var(--spacing-stack-tight);
  --density-cluster: var(--spacing-cluster-tight);
  --density-inset: var(--spacing-inset-compact);
}

.density-default {
  --density-stack: var(--spacing-stack-default);
  --density-cluster: var(--spacing-cluster-default);
  --density-inset: var(--spacing-inset-default);
}

.density-relaxed {
  --density-stack: var(--spacing-stack-loose);
  --density-cluster: var(--spacing-cluster-loose);
  --density-inset: var(--spacing-inset-generous);
}
```

The important thing is not the class names.
The important thing is that density consumes the existing semantic spacing vocabulary.

---

## Decision Rules

When choosing density, ask:

1. Is this context operational or editorial
2. Is scan efficiency more important than atmosphere
3. Does the user need to compare, act, or absorb
4. Is the surrounding page already spatially dense or sparse

If the answer is unclear, choose `default`.

---

## What We Do Not Do

1. No arbitrary “slightly tighter” local overrides.
2. No density decisions made per element instead of per context.
3. No using relaxed density to disguise weak composition.
4. No using compact density to cram too much content into one region.
5. No custom micro-ladders that bypass the spacing system.

---

## Strategic Takeaway

Spacing defines the rhythm vocabulary.
Density defines how tightly that vocabulary is spoken.

That distinction lets Lattice feel flexible without becoming loose.
