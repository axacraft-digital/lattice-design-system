# Lattice — Icons

## Design Intent

Icons are interface primitives, not decorations.

They should feel:

- structural, not ornamental
- consistent across the system, not picked per surface
- legible at the size they appear, not relied on at sizes too small to read
- additive to the label, not a substitute for it

Lattice treats icons the way it treats type, color, and spacing: as a governed primitive consumed from a closed system, not as a per-context choice.

The most common failure mode is the unbounded icon library — Heroicons here, Lucide there, a custom hand-drawn glyph in one footer, and an emoji used because nobody could find the right SVG. The system survives only if the icon vocabulary is bounded the same way the type vocabulary is.

---

## What Counts As An Icon

For the purposes of this system, an "icon" is:

- a small vector glyph used as part of UI structure
- consumed via `currentColor` so it inherits the text color of its context
- sized through the icon size axis defined below
- semantically supportive — never the sole carrier of meaning unless paired with an accessible label

What does **not** count as an icon:

- decorative illustrations
- product photography
- editorial spot illustrations
- brand marks and logos
- emoji used as structural UI elements (forbidden — see below)

These have their own rules and should not be treated as members of the icon system.

---

## One Family Per Layer

The system uses a single icon family per layer of the interface.

Most projects need only one family across the entire surface. When more than one is genuinely required (rare), the families must split along clear layer boundaries:

- one family for navigation, controls, and inline UI
- a different family for marketing illustration or editorial content, if the project genuinely needs that split

What is forbidden is mixing families inside a single layer. A button row with a Lucide search icon, a Heroicons close icon, and a custom SVG arrow is drift, even if each glyph reads correctly on its own.

The picked family should be:

- vector-only (SVG)
- stroked or filled, but consistent within the family
- maintained, not abandoned (an unmaintained set will eventually fall behind on accessibility, sizing, and naming)
- license-clear

---

## Filled vs Outline By Hierarchy

When a family offers both filled and outline variants, treat the choice as a hierarchy decision, not a per-icon decision.

- **Outline** is the default. It reads as inline, structural, and quiet.
- **Filled** signals active or selected state, or a primary visual moment where the icon is doing more than supporting a label.

Rules:

1. Use one style per hierarchy level. Outline icons mixed with filled icons at the same level read as inconsistency, not nuance.
2. Active and selected states may swap from outline to filled to communicate the state change. This is a feature of the system, not an exception.
3. Do not apply filled icons to communicate emphasis on a per-element basis. That is taste, not system.

---

## Stroke Width

When the family is stroke-based, stroke width is a system decision, not a per-icon one.

- Pick one stroke width for the layer. 1.5px or 2px are the typical choices; both are acceptable.
- A denser layer (e.g., compact-mode UI) may use a different stroke width than a relaxed layer, but the difference must be a layer-wide rule, documented in `density.md`, not a per-icon override.
- Never mix stroke widths inside the same component or section.

---

## The Icon Size Axis

Icons are sized through a closed token scale, the same way type is.

```css
:root {
  --icon-xs:  0.875rem;  /* 14px — inline with caption text */
  --icon-sm:  1rem;      /* 16px — inline with body text */
  --icon-md:  1.25rem;   /* 20px — buttons, default UI controls */
  --icon-lg:  1.5rem;    /* 24px — section headers, sidebar nav */
  --icon-xl:  2rem;      /* 32px — feature illustrations, hero supports */
}
```

Rules:

1. Always size icons via the scale. Never write `width: 18px` or `class="h-4 w-4"` peppered through 50 components.
2. Match the icon size to the typographic context it sits in. An icon next to body text uses `--icon-sm`. An icon inside an `md` button uses `--icon-md`.
3. New sizes require a system update. Do not introduce `--icon-2xs` or `--icon-2xl` at a component level.

The size axis is intentionally narrow. Five sizes cover almost every real interface need; the discipline of working within them is what keeps the system legible.

---

## Color and currentColor

Icons consume `currentColor`. They inherit the text color of the element they sit inside.

```css
.icon {
  color: currentColor;
  flex-shrink: 0;
}
```

This means:

- an icon next to body text picks up the body text color automatically
- an icon next to a link picks up the link color
- an icon on a dark surface picks up the dark-surface text color
- a single icon component renders correctly across every theme and every surface without per-context props

Rules:

1. Do not hardcode an icon color. If an icon needs a non-inherited color, either it is wrong, or the surrounding text needs that same color (in which case the parent should set it).
2. Do not introduce icon-specific color tokens. The text color tokens already cover this.
3. Status icons (success, warning, error, info) inherit the status color from their parent or from the alert/badge container — they should not manage that color directly.

---

## Hit Area Is Independent Of Visual Size

This rule is the most commonly broken in practice and the one that matters most for touch interfaces.

The minimum interactive area for any icon-bearing control is **44×44 points**. This is independent of how large the icon glyph itself is. A 16px close icon in a header still requires a 44pt tap target.

Rules:

1. Expand the tap area through padding on the wrapping `<button>` or `<a>`, not by inflating the icon.
2. The visual icon and the hit area are two separate concerns. A small icon inside a generously padded button is correct. An icon stretched to fill a 44pt container is usually wrong.
3. Never rely on browser defaults. The default size of a `<button>` is not 44pt; it is whatever the browser chose, and that is not a contract.
4. This rule is the floor, not the ceiling. Primary CTAs and high-frequency targets should be larger.

---

## Alignment

When an icon sits next to a label, the two must share an optical baseline.

- `display: inline-flex; align-items: center` is the minimum.
- For text-baseline alignment in dense UI, use `vertical-align: text-bottom` on the SVG or set a small negative top margin equal to the typographic optical correction.
- Trust the typographic context. A 16px icon next to 16px body text aligns naturally; a 24px icon next to 16px body text needs an alignment correction or, more often, a smaller icon.

---

## Accessibility

Icons that carry meaning require an accessible label. Icons that are purely decorative must be hidden from assistive technology.

Rules:

1. **Icon-only buttons** must have an `aria-label` describing the action. "X" is not enough; "Close dialog" is.
2. **Decorative icons** must be marked `aria-hidden="true"` or use `role="presentation"` so screen readers skip them.
3. **Icons paired with a visible label** can be marked `aria-hidden="true"` because the label already provides the accessible name. This is the preferred pattern.
4. **Status icons** must not be the sole carrier of meaning. A red error icon without accompanying text fails for users who can't see color or who use a screen reader.

---

## What Is Forbidden

1. **Emoji as structural icons.** Emoji render differently across platforms, do not respect `currentColor`, and break under `prefers-reduced-motion` and high-contrast modes. Emoji are content, not UI.
2. **Raster icons.** PNG and JPG icons do not scale with the type system, do not respect `currentColor`, and produce blurry output at non-1x densities. SVG only.
3. **Per-icon style overrides.** No icon should have its own font-size, color, or stroke width applied at the call site. If a context needs a different icon treatment, that is a layer decision, not a per-icon decision.
4. **Icon-only navigation.** Bottom nav and primary navigation must use both icon and label. Icon-only nav fails accessibility and fails users who don't recognize the glyph.
5. **Decorative arrow icons on every CTA.** An arrow icon should mean direction or forward motion, not "this is a link." If every link has an arrow, the arrow has no meaning.

---

## Recommended API

The component-side shape Lattice consumers should aim for:

```tsx
<Icon name="search" size="md" aria-hidden="true" />

<Button>
  <Icon name="search" size="md" aria-hidden="true" />
  Search
</Button>

<button aria-label="Close dialog">
  <Icon name="x" size="sm" aria-hidden="true" />
</button>
```

These are not mandatory class or component names. They represent the intended closed vocabulary: a single `<Icon>` component, a closed `name` set drawn from one family, a `size` prop drawn from the icon size axis, and an explicit accessibility decision at every call site.

---

## Strategic Takeaway

Icons should be easy to choose and hard to improvise.

The practitioner should answer three questions only:

1. Which name from the family?
2. Which size from the axis?
3. Decorative or meaningful — and if meaningful, what is the accessible label?

Everything else — color, stroke width, alignment, hit area — is already system-defined.
