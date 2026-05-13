# Lattice — Prose System

## Design Intent

Lattice needs a governed answer for unclassed rich text.

Any CMS or Shopify rich text field that outputs raw HTML such as `h2`, `p`, `ul`, `ol`, `strong`, `em`, and `a` must inherit approved system behavior without local styling decisions.

If prose is not defined centrally, every implementation writes its own article styles, rich text styles, and legal copy styles. That is one of the fastest ways a design system drifts.

The prose layer is the bridge between the typography scale and real authored content.

---

## What Prose Is

Prose is a governed container that maps bare HTML elements to existing Lattice type roles, spacing roles, reading measure, and link behavior.

Use it for:

- Shopify rich text fields
- editorial copy blocks
- product education copy
- FAQ answers with sustained paragraphs
- legal or policy content
- article and blog content

Do not use it for:

- tightly composed hero copy
- navigation
- buttons
- structured cards with explicit type classes
- compact UI labels

---

## Container Variants

Lattice defines three prose densities.

### `.prose-sm`

Use for compact supporting copy:

- dense product education
- metadata explanations
- compact legal notes

### `.prose`

The default prose container.

Use for:

- standard rich text sections
- Shopify merchant-authored copy
- FAQ bodies
- general informational content

### `.prose-lg`

Use for premium editorial contexts:

- manifesto copy
- founder-letter sections
- long-form brand narrative
- featured article intros

Only use the large prose size when the section has enough spatial calm to support it.

---

## Core Container Logic

```css
.prose,
.prose-sm,
.prose-lg {
  max-width: var(--measure);
  color: var(--color-text-primary);
}

.prose-sm {
  --prose-body-size: var(--text-sm);
  --prose-body-leading: var(--leading-normal);
  --prose-heading-1-size: var(--text-xl);
  --prose-heading-2-size: var(--text-lg);
  --prose-heading-3-size: var(--text-base);
  --prose-spacing-block: var(--spacing-stack-default);
  --prose-spacing-list: var(--spacing-stack-tight);
}

.prose {
  --prose-body-size: var(--text-base);
  --prose-body-leading: var(--leading-relaxed);
  --prose-heading-1-size: var(--text-2xl);
  --prose-heading-2-size: var(--text-xl);
  --prose-heading-3-size: var(--text-lg);
  --prose-spacing-block: var(--spacing-stack-default);
  --prose-spacing-list: var(--spacing-stack-tight);
}

.prose-lg {
  --prose-body-size: var(--text-lg);
  --prose-body-leading: var(--leading-relaxed);
  --prose-heading-1-size: var(--text-3xl);
  --prose-heading-2-size: var(--text-2xl);
  --prose-heading-3-size: var(--text-xl);
  --prose-spacing-block: var(--spacing-stack-generous);
  --prose-spacing-list: var(--spacing-stack-default);
}
```

The prose container defines the local mapping.
It does not invent new foundational tokens.

---

## Element Mapping

Bare rich text elements should resolve to the following roles:

| Element | Default role |
|--------|--------------|
| `h1` | headline-xl |
| `h2` | headline-lg |
| `h3` | headline-md |
| `h4` | headline-sm |
| `h5` | headline-xs |
| `h6` | headline-xs |
| `p` | body role for current prose variant |
| `ul`, `ol` | body role for current prose variant |
| `li` | body role for current prose variant |
| `strong` | inline emphasis only |
| `em` | italic emphasis only |
| `small` | caption role |
| `blockquote` | large body / editorial pull role |
| `a` | inline link role |
| `code` | mono-caption role with inline surface treatment |

---

## Default Element Styles

```css
.prose :where(p, ul, ol, li),
.prose-sm :where(p, ul, ol, li),
.prose-lg :where(p, ul, ol, li) {
  font-family: var(--font-body);
  font-size: var(--prose-body-size);
  font-weight: var(--weight-regular);
  line-height: var(--prose-body-leading);
  letter-spacing: var(--tracking-normal);
}

.prose :where(h1, h2, h3),
.prose-sm :where(h1, h2, h3),
.prose-lg :where(h1, h2, h3) {
  font-family: var(--font-body);
  font-weight: var(--weight-medium);
  color: var(--color-text-primary);
}

.prose :where(h1),
.prose-sm :where(h1),
.prose-lg :where(h1) {
  font-size: var(--prose-heading-1-size);
  line-height: var(--leading-tight);
}

.prose :where(h2),
.prose-sm :where(h2),
.prose-lg :where(h2) {
  font-size: var(--prose-heading-2-size);
  line-height: var(--leading-tight);
}

.prose :where(h3),
.prose-sm :where(h3),
.prose-lg :where(h3) {
  font-size: var(--prose-heading-3-size);
  line-height: var(--leading-snug);
}

.prose :where(h4, h5, h6),
.prose-sm :where(h4, h5, h6),
.prose-lg :where(h4, h5, h6) {
  font-family: var(--font-body);
  font-size: var(--text-base);
  font-weight: var(--weight-medium);
  line-height: var(--leading-snug);
  color: var(--color-text-primary);
}
```

---

## Spacing Logic

Prose spacing must be structural, not improvised.

```css
.prose > * + *,
.prose-sm > * + *,
.prose-lg > * + * {
  margin-block-start: var(--prose-spacing-block);
}

.prose :where(li + li),
.prose-sm :where(li + li),
.prose-lg :where(li + li) {
  margin-block-start: var(--prose-spacing-list);
}

.prose :where(h1, h2, h3, h4, h5, h6) + :where(p, ul, ol, blockquote),
.prose-sm :where(h1, h2, h3, h4, h5, h6) + :where(p, ul, ol, blockquote),
.prose-lg :where(h1, h2, h3, h4, h5, h6) + :where(p, ul, ol, blockquote) {
  margin-block-start: var(--spacing-stack-tight);
}
```

Rules:

1. Headings pull tighter to the content beneath them.
2. Lists use tighter item spacing than paragraph-to-paragraph spacing.
3. Prose spacing is always stack-driven.
4. No manual margins should be added inside merchant-authored rich text output.

---

## List System

Lists are not undefined browser defaults.

```css
.prose :where(ul),
.prose-sm :where(ul),
.prose-lg :where(ul) {
  padding-inline-start: 1.25em;
  list-style-type: disc;
}

.prose :where(ol),
.prose-sm :where(ol),
.prose-lg :where(ol) {
  padding-inline-start: 1.35em;
  list-style-type: decimal;
}

.prose :where(li > ul, li > ol),
.prose-sm :where(li > ul, li > ol),
.prose-lg :where(li > ul, li > ol) {
  margin-block-start: var(--spacing-stack-tight);
}
```

List rules:

1. Marker color should inherit `--color-text-secondary`.
2. Text remains `--color-text-primary`.
3. Nested lists use the same body size as their parent list.
4. No custom icon bullets unless a component pattern explicitly calls for them.

---

## Inline Elements

```css
.prose :where(strong),
.prose-sm :where(strong),
.prose-lg :where(strong) {
  font-weight: var(--weight-semibold);
  color: var(--color-text-primary);
}

.prose :where(em),
.prose-sm :where(em),
.prose-lg :where(em) {
  font-style: italic;
}

.prose :where(small),
.prose-sm :where(small),
.prose-lg :where(small) {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
}

.prose :where(code),
.prose-sm :where(code),
.prose-lg :where(code) {
  font-family: var(--font-data);
  font-size: 0.92em;
  letter-spacing: 0.02em;
  color: var(--color-text-primary);
  background: var(--color-bg-muted);
  padding-inline: 0.3em;
}
```

---

## Blockquote

Blockquotes need explicit treatment so they do not default to generic browser indentation.

```css
.prose :where(blockquote),
.prose-lg :where(blockquote) {
  font-family: var(--font-body);
  font-size: var(--text-lg);
  font-weight: var(--weight-regular);
  line-height: var(--leading-relaxed);
  color: var(--color-text-primary);
  border-inline-start: 1px solid var(--color-border-strong);
  padding-inline-start: var(--spacing-inset-default);
}

.prose-sm :where(blockquote) {
  font-family: var(--font-body);
  font-size: var(--text-base);
  line-height: var(--leading-relaxed);
  color: var(--color-text-primary);
  border-inline-start: 1px solid var(--color-border-default);
  padding-inline-start: var(--spacing-inset-default);
}
```

Rules:

1. No decorative quotation marks.
2. Emphasis comes from spacing, edge, and type size.
3. Long quotes still obey reading measure.

---

## Links Inside Prose

Links inside rich text need their own behavior. They are not the same as navigation links or standalone action links.

```css
.prose :where(a),
.prose-sm :where(a),
.prose-lg :where(a) {
  color: var(--color-link);
  text-decoration-line: underline;
  text-decoration-thickness: 0.08em;
  text-underline-offset: 0.14em;
}

.prose :where(a:hover, a:focus-visible),
.prose-sm :where(a:hover, a:focus-visible),
.prose-lg :where(a:hover, a:focus-visible) {
  color: var(--color-link-hover);
}
```

Rules:

1. Inline prose links stay underlined by default.
2. Hover changes color before it changes structure.
3. Do not remove underline from inline prose links.
4. This is the inline-link family described in `links.md`, consumed automatically for rich text.

---

## Shopify Rich Text Guidance

Shopify rich text fields usually output unclassed HTML.

That means the implementation pattern should be:

```liquid
<div class="prose">
  {{ section.settings.rich_text }}
</div>
```

If the context is denser or more editorial, use `.prose-sm` or `.prose-lg`.

The container provides the design system. The merchant should not need to think about classes.

---

## Rules

1. Every merchant-authored rich text field must live inside a prose container.
2. Prose defaults to reading measure, not layout width.
3. Bare `p`, `ul`, `ol`, and `blockquote` elements are system-governed, not browser-governed.
4. Inline links inside prose remain underlined by default.
5. List markers are quiet and structural, not decorative.
6. Prose does not invent new tokens; it maps existing typography, spacing, and color tokens to raw content.
7. If a content block needs highly art-directed typography, do not use prose. Build an explicit composition instead.

---

## Strategic Takeaway

Typography defines the scale.
Prose defines how real authored content enters the system.

Without prose, teams will invent article styles locally.
With prose, rich text becomes governed content instead of accidental UI.
