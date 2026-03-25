# Lattice — Section Archetypes

## Purpose

This document defines the approved section families for the Lattice theme.

The design system already defines typography, spacing, grid, color, and components. This file defines how those systems combine into the recurring section structures that make up real pages.

Without section archetypes, the system remains abstract. With section archetypes, page design becomes compositional rather than improvisational.

This document is the bridge between:

- design foundations
- page composition
- theme implementation

---

## How to Use This Document

Each archetype defines:

- the section's job
- the correct frame mode
- the preferred allocation archetype
- the primary spacing behavior
- the typographic hierarchy
- the color/surface logic
- the default density mode
- the default link family
- the default action sizing
- merchant editability boundaries

These are not one-off templates. They are reusable section families.

When designing a new page or section:

1. choose the archetype first
2. adapt the content to the archetype
3. only create a new archetype if the system genuinely cannot express the need

---

## Global Rules

1. Every section must have one clear job.
2. Every section must choose a frame mode explicitly.
3. Every section must use an approved allocation archetype.
4. Merchant editability must be constrained to content, not design-system decisions.
5. A section should feel like a member of the Lattice system even before content is filled in.
6. If a section needs multiple competing jobs, it should probably be split into two sections.

---

## Archetype 1: Hero Statement

### Job

Create the first high-confidence statement of the page:

- what Lattice is
- why it matters
- what the user should do next

This is the page's clearest act of positioning.

### Frame Mode

- `bleed surface` or `wide`

### Allocation Archetype

- `supporting-left`
- `supporting-right`
- `full span`

Choice depends on whether the hero is text-led or image-led.

### Spacing Behavior

- `section-padding-hero`
- internal copy stack uses `stack-tight`, `stack-default`, `stack-loose`
- CTA pair uses `cluster-gap-default`

### Typography

- primary statement uses `heading-display` or `heading-1--serif`
- supporting copy uses `text-lg`
- optional eyebrow uses the mono-label role

### Surface and Color Logic

- often uses `--color-bg-dark` or a full-bleed photographic surface
- text must maintain immediate contrast and clarity
- accent action may appear here, but only once

### Default Density

- `relaxed`

### Default Link Family

- `link-standalone`
- `link-inverse` when the hero sits on a dark surface

### Default Action Sizing

- primary action usually `button--lg`
- secondary action usually `button--md`

### Full-Width Guidance

The hero may be a true 100% full-width surface.

This is the most theatrical section type in the system and is allowed to exceed the normal contained-section feel.

However:

- the content still sits in a governed hero field
- supporting copy must remain readable
- the layout should feel deliberate, not casually centered on an oversized canvas

### Merchant Editability

Editable:

- headline
- supporting copy
- CTA labels and links
- optional media

Locked:

- layout mode
- spacing
- color rhythm
- type treatment

### Notes

The hero is not a content dump. It should feel decisive and sparse.

---

## Archetype 2: Trust Strip

### Job

Establish quick credibility through logos, proof labels, or concise trust markers.

### Frame Mode

- `contained`

### Allocation Archetype

- `full span`

### Spacing Behavior

- `section-padding-compact`
- internal group uses `cluster-gap-loose`

### Typography

- optional mono-label intro
- supporting text should remain quiet and secondary

### Surface and Color Logic

- usually sits on `--color-bg-page`
- logos or trust marks are monochrome

### Default Density

- `compact`

### Default Link Family

- `link-standalone` when a supporting action appears

### Default Action Sizing

- no primary button by default
- if a utility action is present, use `button--sm` or a standalone link

### Merchant Editability

Editable:

- trust items
- logo list
- optional short heading

Locked:

- logo treatment
- section spacing
- visual style

### Notes

This section should feel fast to scan, not like a second hero.

---

## Archetype 3: Section Intro

### Job

Introduce the next chapter of the page with a clear heading and brief orientation copy.

### Frame Mode

- `reading`
- `contained`

### Allocation Archetype

- `narrow center`
- `full span`

### Spacing Behavior

- `section-padding-standard` or `section-padding-generous`
- copy stack uses `stack-tight` and `stack-default`

### Typography

- heading usually `heading-1` or `heading-2`
- supporting copy uses `text-base` or `text-lg`
- mono-label optional

### Surface and Color Logic

- default page surface or alternate light surface

### Default Density

- `default`

### Default Link Family

- `link-inline` inside supporting copy
- `link-standalone` for adjacent low-emphasis actions

### Default Action Sizing

- if an action appears, use `button--md`

### Merchant Editability

Editable:

- heading
- supporting copy
- optional eyebrow

Locked:

- measure
- alignment mode
- type hierarchy

### Notes

Use this when a section needs orientation before payload, not as filler between stronger modules.

---

## Archetype 4: Science Split

### Job

Explain the mechanism, evidence, or product rationale through a composed two-region layout.

### Frame Mode

- `contained`
- `wide`
- occasionally `bleed surface` for dramatic science storytelling

### Allocation Archetype

- `supporting-right`
- `supporting-left`
- `dominant-content`

### Spacing Behavior

- `section-padding-generous`
- intro block and payload separated by `group-gap`
- internal content uses stack semantics

### Typography

- section intro uses `heading-1`, `heading-1--serif`, or `heading-2`
- payload text should respect reading measure even inside a wide region

### Surface and Color Logic

- may use light or dark surfaces depending on narrative emphasis
- dark surfaces should be reserved for stronger proof or mechanism moments

### Default Density

- `relaxed`

### Default Link Family

- `link-inline` inside explanatory copy
- `link-standalone` for related science or evidence actions
- `link-inverse` on dark-surface variants

### Default Action Sizing

- if a CTA appears, default to `button--md`

### Merchant Editability

Editable:

- heading
- body copy
- supporting items or proof points
- optional media

Locked:

- allocation mode
- measure rules
- surface rhythm

### Notes

This archetype is one of the most important in the system. It should feel precise, not salesy.

---

## Archetype 5: Ingredient Grid

### Job

Present ingredients or benefit units as repeated structured content.

### Frame Mode

- `contained`

### Allocation Archetype

- section intro often `supporting-right`
- repeated payload uses `grid`

### Spacing Behavior

- `section-padding-standard` or `section-padding-generous`
- repeated items use `grid-gap-default`
- item internals use `stack-tight` and `stack-default`

### Typography

- intro heading uses `heading-1` or `heading-2`
- item titles use `heading-4`
- supporting copy uses `text-base` or `text-sm`
- labels may use mono style where needed

### Surface and Color Logic

- usually light surface
- cards are optional; ruled/open grid often preferred

### Default Density

- `default`

### Default Link Family

- `link-standalone` for per-item supporting actions
- `link-inline` inside descriptive copy if needed

### Default Action Sizing

- section-level actions use `button--md`
- per-item actions should remain standalone links before becoming buttons

### Merchant Editability

Editable:

- ingredient entries
- names
- descriptions
- optional icons or imagery

Locked:

- grid logic
- item spacing
- containment style

### Notes

Default to open structure before boxed cards. The content should feel clinical and ordered.

---

## Archetype 6: Proof / Stat Band

### Job

Deliver quick, high-contrast proof through metrics, claims, or outcomes.

### Frame Mode

- `bleed surface`
- `contained` inner content

### Allocation Archetype

- `full span`
- sometimes `balanced` for grouped proof units

### Spacing Behavior

- `section-padding-compact` or `section-padding-standard`
- stat groups use cluster/group logic rather than large card spacing

### Typography

- stat numbers use the stat-number role
- labels use mono-label styling

### Surface and Color Logic

- often dark surface
- strong contrast, but no decorative motion

### Default Density

- `compact`

### Default Link Family

- usually no link family inside the proof units
- if supporting actions appear, use `link-inverse`

### Default Action Sizing

- if a section action appears, use `button--md`

### Merchant Editability

Editable:

- stat value
- stat label
- optional short intro

Locked:

- count-up behavior
- surface treatment
- typography treatment

### Notes

This archetype should feel conclusive and fast, not noisy.

---

## Archetype 7: Testimonial Proof

### Job

Provide qualitative proof through customer voice.

### Frame Mode

- `contained`
- `reading` when testimonials are long

### Allocation Archetype

- `grid`
- `narrow center`

### Spacing Behavior

- `section-padding-standard`
- testimonial internals use stack semantics

### Typography

- quote text uses `text-lg` or `text-base`
- attribution is secondary
- context label uses mono role

### Surface and Color Logic

- light surface by default
- cards optional, not mandatory

### Default Density

- `default`

### Default Link Family

- `link-standalone` for secondary proof exploration
- `link-inline` only inside longer quote-adjacent copy

### Default Action Sizing

- no button by default
- if an action is present, keep it at `button--md`

### Merchant Editability

Editable:

- quote
- name
- attribution context

Locked:

- carousel behavior
- quote ornamentation
- presentation style

### Notes

Testimonials are evidence, not decoration. Avoid overproducing them.

---

## Archetype 8: Editorial / Manifesto

### Job

Create a reflective, brand-defining text moment.

### Frame Mode

- `reading`
- sometimes `wide` with reading-measure inner content

### Allocation Archetype

- `narrow center`

### Spacing Behavior

- `section-padding-generous`
- internal stack should feel quiet and spacious

### Typography

- often uses `heading-1--serif`
- body text should remain highly readable and measured

### Surface and Color Logic

- light surface preferred
- color expression comes from restraint, not emphasis

### Default Density

- `relaxed`

### Default Link Family

- `link-inline` inside the copy
- `link-standalone` for adjacent editorial actions

### Default Action Sizing

- if an action appears, use `button--md`

### Merchant Editability

Editable:

- heading
- body copy
- optional supporting media

Locked:

- reading measure
- type hierarchy
- spacing rhythm

### Notes

This is where the brand can feel editorial and elevated without becoming vague or indulgent.

---

## Archetype 9: Conversion CTA

### Job

Close a page or chapter with a focused action.

### Frame Mode

- `contained`
- sometimes `reading` for simpler CTA structures

### Allocation Archetype

- `full span`
- `narrow center`
- occasionally `balanced` for a text/action split

### Spacing Behavior

- `section-padding-standard`
- internal action cluster uses cluster spacing

### Typography

- concise heading
- short supporting copy
- clear action hierarchy

### Surface and Color Logic

- default surface or alternate light surface
- may use accent action if it is the primary conversion moment

### Default Density

- `default`

### Default Link Family

- `link-standalone` for secondary actions

### Default Action Sizing

- primary action usually `button--md`
- use `button--lg` only when the section is intentionally more theatrical

### Merchant Editability

Editable:

- heading
- supporting copy
- CTA labels and links

Locked:

- action hierarchy
- spacing
- layout structure

### Notes

This is not a second hero. It is a closing action surface.

---

## Archetype 10: FAQ / Disclosure

### Job

Answer objections or clarify common questions with disciplined disclosure behavior.

### Frame Mode

- `contained`
- `reading` for longer answers

### Allocation Archetype

- `full span`

### Spacing Behavior

- `section-padding-standard`
- rows separated by rules
- internal rhythm stays compact and orderly

### Typography

- question lines use a heading or strong text role
- answers use readable body text and may need reading measure

### Surface and Color Logic

- quiet light surface preferred

### Default Density

- `compact`

### Default Link Family

- `link-inline` inside longer answers
- no standalone links by default

### Default Action Sizing

- no button by default

### Merchant Editability

Editable:

- questions
- answers

Locked:

- disclosure behavior
- icon treatment
- rhythm and separation logic

### Notes

Use `<details>` / `<summary>` patterns. This archetype should feel functional, not animated for spectacle.

---

## Page Composition Guidance

Archetypes should be combined with restraint.

### Default Page Logic

A strong Lattice page usually moves through a sequence such as:

1. Hero Statement
2. Trust Strip
3. Science Split or Ingredient Grid
4. Proof / Stat Band or Testimonial Proof
5. Editorial / Manifesto or FAQ
6. Conversion CTA

Not every page uses every archetype, but most high-quality pages follow a similar progression:

- position
- validate
- explain
- prove
- convert

---

## Creation Rule

Do not create a new section type just because the content is new.

First ask:

1. Which archetype does this belong to?
2. What is the actual job of the section?
3. Can the current system express it by changing content rather than structure?

Only add a new archetype if the answer is genuinely no.

---

## Strategic Takeaway

A mature design system does not begin page design from blank canvases.

It begins from approved compositional families.

That is what these archetypes are:

- reusable
- system-aligned
- implementation-friendly
- brand-consistent

They are the grammar of the Lattice theme.
