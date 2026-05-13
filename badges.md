# Lattice — Badges And Tags

## Design Intent

Badges, tags, and pills appear everywhere in commerce:

- product tags
- subscription labels
- collection filters
- proof labels
- low-stock or featured markers

If the system does not define them, teams will make them up fast.

Lattice treats these as compact status or classification primitives, not miniature buttons and not decorative stickers.

---

## Primitive Types

Lattice defines two compact primitives:

1. badge
2. tag

### Badge

A badge is informational and non-interactive.

Use for:

- featured
- patented
- bestseller
- subscribe and save

### Tag

A tag may be informational or interactive depending on context.

Use for:

- filters
- category chips
- removable selections

If interactive, it should inherit the system focus behavior and use real button semantics.

---

## Size Axis

Badges and tags use two sizes:

- `sm`
- `md`

They intentionally stop short of `lg`.
These are compact UI primitives, not primary actions.

```css
:root {
  --tag-height-sm: 1.75rem;
  --tag-height-md: 2rem;
  --tag-padding-inline-sm: var(--space-optical-3);
  --tag-padding-inline-md: var(--space-component-1);
}
```

---

## Base Logic

```css
.badge,
.tag {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-optical-2);
  min-height: var(--tag-height-md);
  padding-inline: var(--tag-padding-inline-md);
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  line-height: 1;
  white-space: nowrap;
  border: 1px solid transparent;
  border-radius: 0;
}
```

These primitives should feel crisp and controlled, not soft or bubbly.

---

## Badge Styles

### Neutral

The default informational badge.

```css
.badge--neutral {
  background: var(--color-bg-muted);
  color: var(--color-text-primary);
  border-color: var(--color-border-default);
}
```

### Accent

Use for warm emphasis, but sparingly.

```css
.badge--accent {
  background: var(--color-bg-accent-subtle);
  color: var(--color-text-primary);
  border-color: transparent;
}
```

### Status

Status badges may consume semantic feedback colors when the content is truly stateful.

Examples:

- out of stock
- limited release
- backordered

Do not use status colors for decorative merchandising.

---

## Tag Styles

Tags use a quieter shell by default because they often appear in clusters.

```css
.tag {
  background: transparent;
  color: var(--color-text-primary);
  border-color: var(--color-border-default);
}

.tag[aria-pressed='true'],
.tag--selected {
  background: var(--color-bg-muted);
  border-color: var(--color-border-strong);
}
```

If interactive:

```css
.tag:focus-visible {
  outline: 2px solid var(--color-focus-ring);
  outline-offset: 2px;
}
```

---

## Size Variants

```css
.badge--sm,
.tag--sm {
  min-height: var(--tag-height-sm);
  padding-inline: var(--tag-padding-inline-sm);
  font-size: var(--text-xs);
}

.badge--md,
.tag--md {
  min-height: var(--tag-height-md);
  padding-inline: var(--tag-padding-inline-md);
  font-size: var(--text-sm);
}
```

Rules:

1. Default to `md`.
2. Use `sm` only in dense rows, card metadata, or product micro-labels.
3. Do not introduce rounded pills as an alternate personality mode.

---

## Composition Rules

1. Badge and tag groups use `--spacing-cluster-tight` or `--spacing-cluster-default`.
2. They should wrap cleanly.
3. Do not overload a product card with too many simultaneous badges.
4. If a label needs to trigger a major action, it is not a badge. It is a button.

---

## Recommended API

```html
<span class="badge badge--neutral badge--md">Patented</span>

<button class="tag tag--md" type="button" aria-pressed="false">
  Caffeine-free
</button>
```

---

## Strategic Takeaway

Badges and tags are small enough that teams usually improvise them.
That is exactly why Lattice should define them.
