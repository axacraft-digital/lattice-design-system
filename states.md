# Lattice — States

## Design Intent

States are the invisible behavioral layer of the interface.

They answer questions practitioners should not have to answer ad hoc:

- what does disabled look like
- how does selected differ from default
- what happens during loading
- what does focus look like on light and dark surfaces
- how dark is a scrim
- what color is text selection

If these decisions are not system-owned, they get recreated inside every primitive and drift immediately.

States are not component variants.
They are cross-cutting rules that apply to buttons, forms, tags, navigation, drawers, and overlays.

---

## State Model

Lattice recognizes these core UI states:

1. default
2. hover
3. focus-visible
4. active
5. selected
6. disabled
7. loading
8. overlay

Not every component uses every state, but every interactive primitive should resolve through this vocabulary.

---

## State Token Layer

The state layer depends on the semantic color system.

```css
:root {
  --state-disabled-opacity: 0.45;
  --state-disabled-cursor: not-allowed;

  --state-focus-ring-width: 2px;
  --state-focus-ring-offset: 2px;

  --color-state-disabled-text: var(--color-text-tertiary);
  --color-state-disabled-border: var(--color-border-default);
  --color-state-disabled-surface: var(--color-bg-muted);

  --color-state-selected-surface: var(--color-bg-muted);
  --color-state-selected-border: var(--color-border-strong);
  --color-state-selected-text: var(--color-text-primary);

  --color-overlay-scrim: color-mix(in oklab, var(--charcoal-900) 72%, transparent);
  --color-overlay-scrim-soft: color-mix(in oklab, var(--charcoal-900) 48%, transparent);

  --color-selection-bg: var(--accent-200);
  --color-selection-text: var(--charcoal-900);
}
```

These tokens are not a replacement for component roles.
They are the state behavior layer that components consume.

---

## Focus-Visible

Focus is mandatory and visible.

```css
:focus-visible {
  outline: var(--state-focus-ring-width) solid var(--color-focus-ring);
  outline-offset: var(--state-focus-ring-offset);
}

.on-dark :focus-visible,
.dark-section :focus-visible {
  outline-color: var(--color-focus-ring-on-dark);
}
```

Rules:

1. Never remove focus outlines without replacing them.
2. Focus uses dedicated focus tokens, not accent colors.
3. Use `:focus-visible`, not `:focus`, for the default visible ring.
4. Focus is a usability layer, not a branding opportunity.

---

## Disabled

Disabled means unavailable, not broken.

```css
[disabled],
[aria-disabled='true'] {
  opacity: var(--state-disabled-opacity);
  cursor: var(--state-disabled-cursor);
}
```

Disabled rules:

1. Disabled elements should remain legible.
2. Disabled should suppress pointer interaction.
3. Disabled should not rely on opacity alone if border or text needs additional clarification.
4. Do not use disabled styling for loading states unless the interaction is genuinely unavailable.

Recommended consumption:

```css
.is-disabled {
  color: var(--color-state-disabled-text);
  border-color: var(--color-state-disabled-border);
  background: var(--color-state-disabled-surface);
}
```

---

## Selected

Selected is different from hover.
It indicates a persistent choice or active filter state.

```css
.is-selected,
[aria-pressed='true'],
[aria-selected='true'] {
  color: var(--color-state-selected-text);
  background: var(--color-state-selected-surface);
  border-color: var(--color-state-selected-border);
}
```

Use for:

- filter tags
- segmented controls
- current option selectors
- active view toggles

Do not use selected styling for page-level current navigation unless the navigation system explicitly defines it.

---

## Active / Pressed

Active is transient.
Selected is persistent.

Rules:

1. Active may darken or tighten contrast slightly.
2. Active should not create large motion or scale effects.
3. The difference between hover and active should be subtle but real.

Example:

```css
.button:active {
  filter: brightness(0.96);
}
```

Keep this restrained.
No “pressed in” skeuomorphic treatment.

---

## Loading

Loading is permitted, but it should be quiet and layout-stable.

Rules:

1. Preserve the width of the triggering control.
2. Preserve the label if possible.
3. Prefer inline progress indicators over dramatic spinners.
4. Do not skeleton every interface by default.
5. Loading is not an excuse to hide structure.

Recommended pattern:

```css
.is-loading {
  cursor: progress;
}

.is-loading .loading-indicator {
  inline-size: 1em;
  block-size: 1em;
}
```

For buttons:

- keep text visible if space allows
- if text must be replaced, preserve button width
- suppress repeat clicks while the request is active

---

## Overlay And Scrim

Overlays need a defined atmosphere.
Otherwise every modal and drawer lands with a different darkness level.

```css
.overlay-scrim {
  background: var(--color-overlay-scrim);
}

.overlay-scrim--soft {
  background: var(--color-overlay-scrim-soft);
}
```

Use:

- `--color-overlay-scrim` for modal/dialog contexts
- `--color-overlay-scrim-soft` for drawers or lighter temporary layers

Rules:

1. Scrims darken the world behind the layer. They do not tint it with decorative brand color.
2. Blur is optional, not required.
3. Do not vary scrim opacity arbitrarily per feature.

---

## Text Selection

User text selection is part of the interface polish layer and should be system-owned.

```css
::selection {
  background: var(--color-selection-bg);
  color: var(--color-selection-text);
}
```

This should feel visible, warm, and readable, not neon.

---

## State Ownership

Each layer owns different responsibilities:

- `colors.md` owns the semantic state tokens
- `states.md` owns meaning and cross-component rules
- `motion.md` owns timing and transition behavior
- primitive files own how a specific component consumes the state layer

This keeps state logic from fragmenting into local exceptions.

---

## Rules

1. Hover is never the only signal of interactivity.
2. Focus is always visible for keyboard users.
3. Disabled and loading are not interchangeable.
4. Selected means persistent choice, not temporary contact.
5. Scrims use system tokens, not arbitrary alpha values.
6. State logic should be token-driven before it becomes component-specific.

---

## Strategic Takeaway

If typography is the voice and spacing is the rhythm, states are the reflexes.

They are not glamorous, but they are where systems either feel coherent or quietly fall apart.
