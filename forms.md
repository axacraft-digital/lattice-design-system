# Lattice — Forms

## Design Intent

Form controls should feel like members of the same family as buttons.

That means inputs, selects, textareas, and labels should share:

- the same size axis
- the same control heights where applicable
- the same type logic
- the same focus behavior
- the same restraint

Forms are precision UI, not branding theater.

---

## Form Architecture

The form layer is built from four primitives:

1. field label
2. field control
3. help text
4. error text

Everything else is composition.

If a form system does not define these four pieces, teams will improvise each one locally.

---

## Shared Size Axis

Forms use the same size axis as buttons:

- `sm`
- `md`
- `lg`

This ensures inline rows such as input plus submit button stay visually aligned.

```css
.field__control--sm {
  min-height: var(--control-height-sm);
  padding-inline: var(--control-padding-inline-sm);
  font-size: var(--control-text-sm);
}

.field__control--md {
  min-height: var(--control-height-md);
  padding-inline: var(--control-padding-inline-md);
  font-size: var(--control-text-md);
}

.field__control--lg {
  min-height: var(--control-height-lg);
  padding-inline: var(--control-padding-inline-lg);
  font-size: var(--control-text-lg);
}
```

Default to `md`.

---

## Field Label

Labels are explicit. They do not rely on placeholders to do their job.

```css
.field__label {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  line-height: var(--leading-normal);
  color: var(--color-text-primary);
}
```

Rules:

1. Labels sit above controls.
2. Labels use the `label` type role.
3. Required indicators should be quiet, not alarmist.

---

## Field Control

```css
.field__control {
  inline-size: 100%;
  min-height: var(--control-height-md);
  padding-inline: var(--control-padding-inline-md);
  font-family: var(--font-body);
  font-size: var(--control-text-md);
  font-weight: var(--weight-regular);
  color: var(--color-text-primary);
  background: var(--color-bg-page);
  border: 1px solid var(--color-border-default);
  border-radius: 0;
}

.field__control::placeholder {
  color: var(--color-text-tertiary);
}

.field__control:focus-visible {
  outline: 2px solid var(--color-focus-ring);
  outline-offset: 2px;
}
```

Rules:

1. Inputs are square-cornered.
2. Placeholder text is supplemental only.
3. Border contrast stays quiet until focus.

---

## Textarea

Textareas belong to the same family, but height is content-driven rather than fixed.

```css
textarea.field__control {
  min-block-size: calc(var(--control-height-md) * 3);
  padding-block: var(--space-optical-3);
  resize: vertical;
}
```

Rules:

1. Do not constrain textareas to button-like heights.
2. Resize is vertical only.

---

## Selects

Selects should not become special snowflakes.
They use the same control shell as inputs.

Rules:

1. Same size axis as inputs and buttons.
2. Same label role.
3. Same focus treatment.

If a custom chevron is used, it should be monochrome and inherit current text color.

---

## Help and Error Text

```css
.field__help {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--weight-regular);
  line-height: var(--leading-normal);
  color: var(--color-text-secondary);
}

.field__error {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  line-height: var(--leading-normal);
  color: var(--color-status-error);
}
```

Rules:

1. Help text is supportive and secondary.
2. Error text is concise and direct.
3. Do not use placeholder text to convey validation requirements.

---

## Field Stack

The standard field stack is:

```text
[label]
  ↕ stack-tight
[control]
  ↕ stack-tight
[help or error]
```

Use spacing tokens, not local margins.

---

## Inline Control Rows

Inline control rows are common in commerce:

- email capture plus submit button
- quantity plus add-to-cart
- filter dropdowns

Rules:

1. Every control in the row uses the same size token.
2. Row spacing uses `--spacing-cluster-default`.
3. Default to `md`.
4. If the row becomes cramped on mobile, stack it rather than squeezing the controls.

---

## Disabled and Invalid States

```css
.field__control:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.field__control[aria-invalid='true'] {
  border-color: var(--color-status-error);
}
```

This is intentionally restrained.
The full state token system can evolve later without changing the form model.

---

## Recommended API

```html
<div class="field">
  <label class="field__label" for="email">Email address</label>
  <input class="field__control field__control--md" id="email" type="email" placeholder="you@example.com">
  <p class="field__help">We'll send product updates and research notes.</p>
</div>
```

---

## Strategic Takeaway

Lattice forms should not force practitioners to decide what a label looks like, how tall a control should be, or whether an inline field row aligns with a button.

Those decisions belong to the system.
