# Lattice — Buttons

## Design Intent

Buttons are action primitives, not decorative objects.

They should feel:

- calm
- decisive
- structurally aligned with form controls
- visually governed by semantic action roles

Lattice buttons are defined by two axes:

1. role
2. size

This prevents teams from inventing ad hoc button variants like `button-small-dark`, `cta-hero`, or `ghost-pill`.

---

## Button Axes

### Role Axis

Lattice defines three button roles:

- `primary`
- `secondary`
- `accent`

These map to the semantic color system.

### Size Axis

Lattice defines three button sizes:

- `sm`
- `md`
- `lg`

The size axis is shared with inputs and other compact interactive primitives.

Size is not just height.
It governs:

- control height
- horizontal padding
- text role
- icon size
- icon-to-label gap

---

## Shared Size Tokens

```css
:root {
  --control-height-sm: 2.5rem;
  --control-height-md: 3rem;
  --control-height-lg: 3.5rem;

  --control-padding-inline-sm: var(--space-component-2);
  --control-padding-inline-md: var(--space-component-3);
  --control-padding-inline-lg: var(--space-component-4);

  --control-text-sm: var(--text-sm);
  --control-text-md: var(--text-sm);
  --control-text-lg: var(--text-base);

  --control-gap-sm: var(--space-optical-2);
  --control-gap-md: var(--space-optical-2);
  --control-gap-lg: var(--space-optical-3);
}
```

This token layer keeps the size model portable across buttons, inputs, selects, and tags where appropriate.

---

## Base Button Logic

```css
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--control-gap-md);
  min-height: var(--control-height-md);
  padding-inline: var(--control-padding-inline-md);
  font-family: var(--font-sans);
  font-size: var(--control-text-md);
  font-weight: var(--weight-medium);
  line-height: 1;
  text-align: center;
  text-decoration: none;
  border: 1px solid transparent;
  border-radius: 0;
  white-space: nowrap;
}
```

Buttons are square-cornered by default.
They rely on color, type, and spacing for character rather than soft geometry.

---

## Button Roles

### Primary

Use for the default high-confidence action in a local context.

```css
.button--primary {
  background: var(--color-action-primary-bg);
  color: var(--color-action-primary-text);
}
```

### Secondary

Use as the companion action to a primary or accent action.

```css
.button--secondary {
  background: var(--color-action-secondary-bg);
  color: var(--color-action-secondary-text);
  border-color: var(--color-action-secondary-border);
}
```

### Accent

Use only for the strongest conversion action in a local context.

```css
.button--accent {
  background: var(--color-action-accent-bg);
  color: var(--color-action-accent-text);
}
```

Role rules:

1. One accent button maximum per local action cluster.
2. A section should rarely contain more than one primary decision and one supporting decision.
3. If every action becomes accent, the role has failed.

---

## Button Sizes

### Small

Use for:

- compact inline toolbars
- card footers
- utility actions
- dense filter bars

```css
.button--sm {
  min-height: var(--control-height-sm);
  padding-inline: var(--control-padding-inline-sm);
  gap: var(--control-gap-sm);
  font-size: var(--control-text-sm);
}
```

### Medium

The default button size.

Use for:

- standard CTAs
- form submission
- navigation actions

```css
.button--md {
  min-height: var(--control-height-md);
  padding-inline: var(--control-padding-inline-md);
  gap: var(--control-gap-md);
  font-size: var(--control-text-md);
}
```

### Large

Use for:

- hero CTAs
- section-leading conversion actions
- deliberate editorial callouts

```css
.button--lg {
  min-height: var(--control-height-lg);
  padding-inline: var(--control-padding-inline-lg);
  gap: var(--control-gap-lg);
  font-size: var(--control-text-lg);
}
```

Size rules:

1. Default to `md`.
2. Use `lg` only when the surrounding composition can support the larger action.
3. Do not create an `xs` or `xl` without updating the system spec.

---

## Buttons With Icons

Icons are optional, not default.

If used:

- they inherit `currentColor`
- they follow the shared size axis
- they sit before the label unless the interaction clearly implies forward motion

```css
.button--sm .button__icon {
  inline-size: 1rem;
  block-size: 1rem;
}

.button--md .button__icon {
  inline-size: 1rem;
  block-size: 1rem;
}

.button--lg .button__icon {
  inline-size: 1.125rem;
  block-size: 1.125rem;
}
```

Rules:

1. Do not use icon-only buttons as the default answer for actions that require text clarity.
2. Do not add decorative arrow icons to every CTA.
3. The icon should clarify direction or function, not decorate the label.

---

## Interaction Behavior

Buttons need defined interactive behavior, even before the full states file exists.

```css
.button:hover {
  transition:
    background-color 160ms ease,
    color 160ms ease,
    border-color 160ms ease;
}

.button--primary:hover {
  background: var(--color-action-primary-hover);
}

.button--secondary:hover {
  background: var(--color-action-secondary-hover-bg);
  color: var(--color-action-secondary-hover-text);
}

.button--accent:hover {
  background: var(--color-action-accent-hover);
}

.button:focus-visible {
  outline: 2px solid var(--color-focus-ring);
  outline-offset: 2px;
}
```

### Disabled

```css
.button[disabled],
.button[aria-disabled='true'] {
  opacity: 0.45;
  cursor: not-allowed;
  pointer-events: none;
}
```

### Loading

Loading is permitted, but it should be quiet.

Rules:

1. Keep the button width stable while loading.
2. Preserve the text label if possible.
3. Do not replace every loading action with a spinning icon by default.

---

## Composition Rules

1. Maximum two buttons in a local action cluster.
2. Button pairs use `--spacing-cluster-default`, not arbitrary margins.
3. Buttons are sentence case, not uppercase.
4. Buttons and inputs sharing a row must use the same size token.
5. On dark surfaces, the primary action may invert for contrast, but it remains a semantic primary action.

---

## Recommended API

```html
<a class="button button--primary button--md" href="/products/brain-ritual">
  Shop now
</a>

<button class="button button--secondary button--sm" type="button">
  Learn more
</button>
```

---

## Strategic Takeaway

Lattice buttons should be easy to choose and hard to improvise.

The practitioner should answer two questions only:

1. What role is this action?
2. What size context is it in?

Everything else should already be system-defined.
