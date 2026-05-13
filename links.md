# Lattice — Links

## Design Intent

Not every link is the same kind of object.

Lattice needs to distinguish between:

- links inside body copy
- standalone utility links
- navigational links
- links on dark surfaces

If all anchors share one treatment, teams will start stripping underlines from prose, over-styling nav links, and inventing footer variants locally.

Links are not mini-buttons.
They are text-level interactive elements with distinct jobs.

---

## Link Families

Lattice defines four link families:

1. inline link
2. standalone link
3. nav link
4. inverse link

These are role distinctions, not decorative options.

---

## Token Layer

Links should consume semantic link tokens rather than local text colors.

```css
:root {
  --color-link: var(--charcoal-900);
  --color-link-hover: var(--stone-600);
  --color-link-visited: var(--charcoal-900);

  --color-link-nav: var(--charcoal-900);
  --color-link-nav-hover: var(--stone-600);
  --color-link-nav-current: var(--charcoal-900);

  --color-link-on-dark: var(--neutral-100);
  --color-link-on-dark-hover: var(--stone-300);

  --link-underline-thickness: 0.08em;
  --link-underline-offset: 0.14em;
}
```

The underline values are shared so link behavior feels related even when the roles differ.

---

## Inline Links

Inline links live inside prose and body copy.

They are governed by clarity first.

```css
.link-inline {
  color: var(--color-link);
  text-decoration-line: underline;
  text-decoration-thickness: var(--link-underline-thickness);
  text-underline-offset: var(--link-underline-offset);
}

.link-inline:hover,
.link-inline:focus-visible {
  color: var(--color-link-hover);
}
```

Rules:

1. Inline links stay underlined by default.
2. Hover should strengthen or shift color before changing structure.
3. Do not remove underline from inline prose links.
4. Inline links should not adopt button-like spacing or borders.

`prose.md` consumes this family automatically for raw rich text.

---

## Standalone Links

Standalone links are independent text actions outside running copy.

Use for:

- small calls to continue reading
- utility actions in cards
- low-emphasis adjacent actions
- editorial “read more” patterns

```css
.link-standalone {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-cluster-tight);
  color: var(--color-link);
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  line-height: var(--leading-normal);
  text-decoration: none;
}

.link-standalone:hover,
.link-standalone:focus-visible {
  color: var(--color-link-hover);
  text-decoration-line: underline;
  text-decoration-thickness: var(--link-underline-thickness);
  text-underline-offset: var(--link-underline-offset);
}
```

Rules:

1. Standalone links may reveal underline on hover.
2. They should feel lighter than buttons.
3. If the action carries primary decision weight, use a button instead.

---

## Nav Links

Navigation links are structural orientation elements, not prose links.

```css
.link-nav {
  color: var(--color-link-nav);
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  line-height: var(--leading-normal);
  text-decoration: none;
}

.link-nav:hover,
.link-nav:focus-visible {
  color: var(--color-link-nav-hover);
}

.link-nav[aria-current='page'],
.link-nav.is-current {
  color: var(--color-link-nav-current);
  text-decoration-line: underline;
  text-decoration-thickness: 0.06em;
  text-underline-offset: 0.18em;
}
```

Rules:

1. Nav links do not use persistent underline unless current.
2. Current-page indication should be quiet but unmistakable.
3. Do not make every nav item look like a CTA.

---

## Inverse Links

Inverse links are used on dark surfaces.

They may be inline, standalone, or navigational, but they consume the dark-surface token family.

```css
.link-inverse {
  color: var(--color-link-on-dark);
}

.link-inverse:hover,
.link-inverse:focus-visible {
  color: var(--color-link-on-dark-hover);
}
```

Rules:

1. Inverse links should remain high-contrast.
2. Do not tint inverse links with accent color by default.
3. The dark-surface treatment changes color, not the basic role logic.

---

## Footer Links

Footer links are usually nav links on dark or low-contrast surfaces.

Use:

- `.link-nav link-inverse`

or

- `.link-standalone link-inverse`

depending on whether the link is structural navigation or a utility action.

This avoids creating a separate “footer link” species.

---

## Icon Usage

Links may use icons more often than buttons, but only with purpose.

Rules:

1. Icons inherit `currentColor`.
2. Icons are supporting direction or function, not decoration.
3. A trailing arrow is acceptable for standalone editorial links, not mandatory for every link.
4. Nav links should rarely need icons.

---

## Visited Links

Visited styling should be restrained.

```css
.link-inline:visited,
.link-standalone:visited {
  color: var(--color-link-visited);
}
```

Lattice does not use loud purple visited links.
Visited state should remain coherent with the palette.

---

## Recommended API

```html
<a class="link-standalone" href="/pages/our-story">Read our story</a>

<a class="link-nav" href="/collections/all" aria-current="page">Shop</a>

<a class="link-standalone link-inverse" href="/pages/science">Science</a>
```

---

## Rules

1. Inline links and standalone links are not interchangeable.
2. Nav links should communicate orientation, not decoration.
3. Inverse links only change surface contrast behavior, not role.
4. If a link starts behaving like a major action, convert it to a button.
5. Do not invent local footer-link or card-link text styles before checking these families.

---

## Strategic Takeaway

Links are one of the fastest points of system drift because they feel too small to document.

That is exactly why Lattice should define them clearly.
