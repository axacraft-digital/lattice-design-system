# Lattice — Grid and Layout

## Design Intent

Lattice's grid is not merely a 12-column layout. It is a responsive compositional field designed to support three things simultaneously:

- cinematic page structure
- disciplined editorial measure
- modular Shopify section composition

The system is influenced by Swiss minimalism, but it is not trying to imitate a corporate presentation deck. The purpose of the grid is to create a layout language that feels precise, calm, and architectural while remaining usable inside a Shopify theme made of sections, blocks, and merchant-editable content.

Like the typography and spacing systems, the grid is designed as a governed model rather than a collection of good-looking defaults.

---

## Grid as a Compositional Field

The grid system operates through five structural ideas:

1. **Canvas** — the maximum field a contained section may occupy
2. **Content** — the normal width for structured section layouts
3. **Reading Measure** — the narrower width for long-form text
4. **Allocation** — how available width is proportioned between major regions
5. **Adaptation** — how layouts simplify when their composition stops being coherent

This means the grid is not defined only by columns. Columns are one implementation tool inside a broader compositional system.

---

## Shared Anchor Conditions

The layout system shares the same viewport anchors as typography and spacing so that the entire design system expands under the same environmental conditions.

```css
:root {
  --viewport-min: 20rem;  /* 320px */
  --viewport-max: 90rem;  /* 1440px */
}
```

This does not mean every layout relationship is fluid in the same way typography is. It means the system is coordinated.

Typography defines hierarchy.
Spacing defines spatial behavior.
Grid defines how content occupies the field those systems create.

---

## Structural Width Regimes

The layout system uses three width regimes, not one generic container.

### 1. Canvas Width

The outer maximum footprint for a contained section.

```css
:root {
  --layout-canvas-max: 100rem;  /* 1600px */
}
```

Use for:

- large structural compositions
- image + text sections
- wide feature panels
- sections that need architectural presence

The canvas defines how wide a section may become before it begins to feel overextended.

For Lattice, the canvas is intentionally wider than a traditional corporate or editorial site. The goal is not generic fluidity. The goal is a more theatrical desktop field that gives photography, hero statements, and premium composition more visual punch.

---

### 2. Content Width

The standard width for structured section content.

```css
:root {
  --layout-content-max: 75rem;  /* 1200px */
}
```

Use for:

- ingredient grids
- two-region information sections
- testimonial layouts
- CTA sections
- repeated content structures

This is the main working field for most sections.

The content width remains disciplined even as the canvas expands. This is a deliberate separation:

- the **canvas** creates drama
- the **content field** preserves structure
- the **reading field** preserves legibility

---

### 3. Reading Width

The constrained width for prose-heavy content and explanatory text.

```css
:root {
  --layout-reading-max: 42rem;  /* ~672px */
}
```

Use for:

- manifesto copy
- scientific explanation blocks
- long testimonial or founder-note content
- editorial intros
- FAQ answers and explanatory text clusters

This is a critical distinction. Not all text should live at content width simply because the section itself is wide.

This is especially important now that the canvas is wider. The wider field is for composition, not for unchecked line length.

---

## Fluid Containment and Insets

The grid does not use static edge padding. Containment is fluid and tied to the same responsive logic as the rest of the system.

```css
:root {
  --layout-inset-inline: clamp(1.25rem, 1.036rem + 1.071vw, 2rem);      /* 20 → 32px */
  --layout-inset-inline-wide: clamp(1.5rem, 1.179rem + 1.607vw, 3rem);  /* 24 → 48px */
}
```

### Why Two Inset Modes Exist

`--layout-inset-inline` is the default containment rule.

`--layout-inset-inline-wide` is used when the composition should feel more editorial or architectural, especially on wide screens where extra edge breathing room improves perceived quality.

This allows the system to frame content differently without inventing arbitrary per-section padding rules.

---

## Layout Frames

Sections use one of four frame modes.

### Contained Frame

The outer wrapper is constrained to the canvas width and padded by the default inline inset.

Use for:

- standard information sections
- ingredient features
- testimonials
- CTA blocks

### Wide Frame

The outer wrapper is constrained to the canvas width but uses the wide inline inset.

Use for:

- premium editorial moments
- hero-adjacent composition
- sections that need more atmospheric edge spacing

### Reading Frame

The section content aligns to reading width rather than content width.

Use for:

- manifesto copy
- explanatory science sections
- letter-style or essay-like surfaces

### Bleed Surface

The section background or media runs full-bleed, but the inner content remains aligned to content width or reading width.

Use for:

- hero sections
- dark proof bands
- large visual storytelling surfaces

Full-bleed surfaces are allowed. Unconstrained full-bleed content is not.

For standard bleed surfaces, inner content should still align to content width or reading width. However, the hero section is a special case: it may use a wider, more theatrical content field than standard contained sections, provided that the content placement remains intentional and bounded.

---

## Allocation Archetypes

Instead of documenting a loose set of "common layouts," the system defines a small set of semantic allocation archetypes.

These are not just percentages. They are compositional modes.

### Full Span

Single-region layout aligned to content width or reading width.

Use for:

- hero copy
- centered editorial sections
- simple CTA blocks
- trust strips

```css
grid-template-columns: minmax(0, 1fr);
```

---

### Narrow Center

Single-region layout constrained to reading width and centered within the content field.

Use for:

- manifesto copy
- section intros
- scientific explanation blocks
- long testimonial statements

This is the preferred layout for any section where text clarity matters more than structural width.

---

### Balanced Split

Two equal regions.

Use for:

- comparison blocks
- image + text when both sides have equal visual importance
- paired content panels

```css
grid-template-columns: repeat(2, minmax(0, 1fr));
```

---

### Supporting Right

Left region introduces. Right region carries denser or more extensive content.

This is the default Lattice split.

Use for:

- heading left + body/specs right
- ingredient section intros
- science section intros with denser supporting content

```css
grid-template-columns: 5fr 7fr;
```

This is more than a ratio. It encodes a relationship: orientation on the left, payload on the right.

---

### Supporting Left

Right region introduces. Left region carries denser or more extensive content.

Use for:

- image right + copy left
- visual emphasis on the right with explanatory material on the left
- alternating page rhythm

```css
grid-template-columns: 7fr 5fr;
```

---

### Dominant Content

One region materially outweighs the other.

Use for:

- strong visual support paired with a focused text column
- product detail or science visuals paired with concise explanation
- modular feature storytelling

```css
grid-template-columns: 4fr 8fr;
```

Use sparingly. This is a more forceful compositional move than the standard split.

---

## Region Spacing and Gutters

Gutters are not independent magic numbers. They inherit from the spacing system.

```css
:root {
  --layout-gutter-tight: var(--space-component-2);
  --layout-gutter-default: var(--spacing-grid-gap);
  --layout-gutter-loose: var(--spacing-group-gap);
}
```

### Gutter Semantics

- `tight` — compact metadata rows, smaller grouped regions
- `default` — standard repeated grids and two-region content sections
- `loose` — large editorial or premium split-panel compositions

This keeps the layout system aligned with the spacing system instead of competing with it.

---

## Repeating Grid Behavior

Repeating content grids are a distinct layout primitive. They are not the same as split layouts.

### Principles

1. Repeating grids use the content width, not reading width.
2. Grid gaps come from the component spacing layer, never the layout layer.
3. Cards or repeated items should not become tiny just to preserve column count.
4. Repeating grids collapse by coherence, not by attachment to a desktop column count.

### Default Patterns

#### Three-Up Grid

Use for:

- feature lists
- ingredient highlights
- compact testimonial cards
- trust or proof modules

```css
grid-template-columns: repeat(3, minmax(0, 1fr));
gap: var(--layout-gutter-default);
```

#### Two-Up Grid

Use for:

- paired feature explanations
- larger testimonial or quote cards
- image/text cards with more content density

```css
grid-template-columns: repeat(2, minmax(0, 1fr));
gap: var(--layout-gutter-default);
```

#### Single Column

Use for:

- dense content
- narrow containers
- mobile collapse
- editorial sections where readability takes priority over scanability

---

## Context-Aware Adaptation

The system adapts by compositional coherence, not only viewport width.

This is the layout equivalent of the new spacing model's behavioral layers.

### Adaptation Principles

1. A layout should remain split only while both regions still feel intentional.
2. Repeating grids should reduce column count before card widths become weak.
3. Text-heavy sections should shift to reading-measure layouts earlier than visually driven sections.
4. Collapse decisions should be based on available field width, not loyalty to desktop structure.

### Container-Aware Thinking

Even if initial implementation uses viewport media queries, the design model should think in terms of container width.

That means asking:

- does this module still have enough width to sustain its allocation archetype?
- has the reading measure become too wide or too narrow?
- should this repeated grid become two-up or one-up based on its actual field, not the entire viewport?

This is the correct long-term mindset for modular storefront design.

---

## Adaptation by Archetype

### Full Span

Never becomes multi-column. It may shift from content width to reading width if readability requires it.

### Narrow Center

Remains single-region at all widths. The only change is available inset and surrounding page rhythm.

### Balanced Split

Can hold longer than asymmetric layouts because both regions have equal weight. It collapses when either side becomes too narrow to preserve a clear bilateral relationship.

### Supporting Right / Supporting Left

These collapse earlier than balanced splits if both regions are text-heavy. If one side is primarily visual, they may hold longer.

### Dominant Content

This can hold at wider tablet widths if the secondary region is concise. If both regions require dense reading, it should collapse earlier.

This logic is more important than any single breakpoint number.

---

## Reading Measure Integration

The reading width is not a special-case exception. It is a core part of the layout system.

### Reading-First Rule

If a section contains sustained prose, explanation, or narrative content, constrain the copy to reading measure even if the section itself occupies a wider frame.

### Examples

- A science section may use a wide split layout overall, but the explanatory paragraph block inside the supporting region should still honor reading measure.
- A founder note inside a contained section should use a reading frame, not a full content-width frame.
- A testimonial quote can live in a larger layout field, but the quote text itself should not stretch to the full structural width.

This is one of the main differences between a sophisticated layout system and a merely responsive one.

---

## Full-Bleed vs. Contained Surfaces

### Full-Bleed Surfaces

Allowed for:

- hero backgrounds
- dark bands
- editorial photography panels
- atmospheric proof sections

Rules:

1. The surface may bleed edge-to-edge.
2. Inner content aligns to content width or reading width.
3. Full-bleed does not mean "content can ignore the field."

### Hero Full-Bleed Exception

The hero may use a true 100% full-width surface with a wider inner content field than the rest of the system.

This is intentional.

The hero is the one place where the site is allowed to feel most cinematic and spatially expansive.

Rules:

1. The media or surface may run fully edge-to-edge.
2. The hero content field may exceed normal content width.
3. The content still requires a bounded alignment logic. It should feel composed, not freely floating.
4. Reading comfort still applies to longer supporting copy even inside a wider hero field.

### Contained Surfaces

Used for:

- text-heavy sections
- product explanation modules
- ingredient and benefit sections
- testimonials
- CTA structures

Rules:

1. Align to canvas width with fluid inset.
2. Use semantic allocation archetypes instead of ad hoc split ratios.
3. Constrain prose-heavy content to reading measure where needed.

---

## Layout Primitives

These are the mental building blocks the system expects theme sections to use.

### Frame

Defines the outer containment mode:

- contained
- wide
- reading
- bleed surface

### Region

A major content area within a section.

### Split

A two-region composition using one of the allocation archetypes.

### Grid

A repeating-item structure using content width and component-layer gutters.

### Measure

A readable line-length constraint applied inside wider structural fields.

This is the compositional vocabulary between design and implementation.

---

## Practical Usage Examples

### Standard Information Section

Frame:
- contained

Allocation:
- supporting-right

Spacing:
- `section-padding-standard`
- `group-gap`
- `layout-gutter-default`

This is the default Lattice section shape.

---

### Editorial Science Section

Frame:
- wide or bleed surface

Allocation:
- supporting-left or dominant-content

Inner text:
- constrained to reading measure

Spacing:
- `section-padding-generous`

This creates a more cinematic section without sacrificing readability.

---

### Trust Strip

Frame:
- contained

Allocation:
- full span

Content behavior:
- clustered row, horizontally centered

Spacing:
- `section-padding-compact`

This is a simple compositional unit. Do not over-structure it.

---

### Centered Manifesto Block

Frame:
- reading

Allocation:
- narrow-center

Spacing:
- `section-padding-generous`

This is the preferred pattern for brand statements and reflective editorial copy.

---

### Repeating Feature Grid

Frame:
- contained

Allocation:
- grid

Columns:
- three-up when coherent
- two-up when the field narrows
- single column when readability and card integrity require it

Spacing:
- `layout-gutter-default`

---

## Relationship to Spacing

Spacing answers:

- what kind of space this is
- how much it should grow
- whether it belongs to optical, component, or layout behavior

Grid answers:

- what kind of field this content occupies
- how the field is allocated
- when the composition should simplify

Spacing and grid are therefore parallel systems:

- spacing governs rhythm
- grid governs occupation

The grid system should never invent its own private spacing logic where the spacing system already provides one.

---

## Relationship to Typography

Typography sets hierarchy and measure expectations.

Grid determines how those typographic elements are placed in space.

The key relationships are:

- reading measure protects typographic comfort
- content width supports structured information
- canvas width supports architectural section composition
- allocation archetypes give the hierarchy a spatial expression

Typography without grid becomes centered text on a wide page.
Grid without typography becomes structure without voice.

The two systems must remain coordinated.

---

## Rules

1. Do not treat the grid as "12 columns everywhere." Use the column field as an implementation aid, not the entire design concept.
2. Every section must choose an explicit frame mode: contained, wide, reading, or bleed surface.
3. Every two-region section must use an allocation archetype: balanced, supporting-right, supporting-left, or dominant-content.
4. Long-form text should default to reading measure, not content width.
5. Repeating grids use component-layer gutters, not layout-layer spacing.
6. Full-bleed is allowed for surfaces, never for unconstrained content.
7. Layouts should collapse when their composition stops being coherent, not because a generic desktop pattern is being defended too long.
8. If a section needs a new allocation mode beyond the approved archetypes, that is a design-system decision, not a one-off implementation choice.

---

## Strategic Takeaway

A basic responsive system asks:

"How many columns should this have at tablet?"

A sophisticated compositional system asks:

- what field should this content occupy?
- what width regime does it belong to?
- what relationship exists between the regions?
- when does that relationship stop being coherent?

Lattice's grid system is designed to answer those questions directly.
