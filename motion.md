# Lattice — Motion and Interaction

## Design Intent

Motion in Lattice is functional, not decorative. Every animation serves one of two purposes: providing feedback on user interaction (hover, focus, click) or gently introducing content as the user scrolls.

The governing principle is "noticed but not noticed" — transitions should feel natural enough that the user doesn't consciously register them, but their absence would make the site feel static and unresponsive.

Swiss minimalism calls for restraint. No parallax, no particle effects, no animated backgrounds, no scroll-jacking.

---

## Timing Tokens

```css
:root {
  --duration-fast: 120ms;       /* Micro-interactions: hover color shifts, focus rings */
  --duration-normal: 200ms;     /* Standard transitions: button hovers, nav state changes */
  --duration-slow: 350ms;       /* Larger transitions: section reveals, accordion open/close */
  --duration-entrance: 500ms;   /* Content entrance animations on scroll */
}
```

---

## Easing Functions

```css
:root {
  --ease-default: cubic-bezier(0.25, 0.1, 0.25, 1);    /* Subtle ease-out — most transitions */
  --ease-in-out: cubic-bezier(0.42, 0, 0.58, 1);        /* Symmetric — accordion, reveals */
  --ease-out: cubic-bezier(0, 0, 0.2, 1);                /* Decelerate — entrance animations */
}
```

Use `--ease-default` for everything unless there's a specific reason not to. Never use `linear` for UI transitions (it feels mechanical).

---

## Motion Contracts

These are the system-wide rules that govern *every* animation in the interface, not just one category. A new motion that violates these rules is a finding, regardless of how good it looks in isolation.

### 1. Reduced motion is a system-wide contract

Every animation must honor `prefers-reduced-motion: reduce`. This is not a special case for scroll entrances; it applies to every transition in the system — hover shifts, focus rings, accordions, route transitions, modal sheets, drag feedback, page reveals.

The implementation rule is the same in every case: when reduced motion is requested, the visual end state still arrives, but instantly and without animation. Content is not hidden because the user opted out; the animation simply collapses to zero duration.

Practitioners working in code-side tooling (React, Vue, Svelte) should expose this through a single hook or utility (e.g., a `useReducedMotion()` wrapper) so that every animated component consumes it the same way. There should not be one component that respects the preference and another that ignores it.

### 2. Exit is shorter than enter

Exit animations should run at 60–70% of the corresponding enter duration.

The reason is perceptual: entering content is the user's reward and benefits from being given a moment. Exiting content is friction and should resolve quickly. Symmetric durations make exits feel slow even when the math is identical.

This applies to modals closing, drawers retracting, dropdowns dismissing, and any state transition with both an open and a close phase.

### 3. Modals and sheets animate from their trigger source

When a modal, sheet, drawer, or popover opens, the animation should originate from the element that triggered it — not from the screen edge or the center of the viewport.

This preserves spatial continuity. The user understands that the new surface came from somewhere they pointed at, which makes dismissal feel reversible rather than disorienting.

In practice this usually means a small scale and translate from the trigger's bounding box to the surface's resting position, or a directional slide from the trigger side.

### 4. Direction expresses hierarchy

When transitioning between routes or hierarchical states, direction is meaningful and consistent:

- **Forward / deeper:** content enters from the right or below, exits to the left or above.
- **Back / shallower:** content enters from the left or above, exits to the right or below.

This is a small rule with outsized effect. Once the user's eye has learned the pattern, navigation feels structurally legible without any explanation.

Lateral transitions (sibling routes at the same hierarchy level) should use crossfade rather than direction, so direction is reserved for hierarchy changes.

### 5. Animations are interruptible

A user action during an animation must be respected immediately. If the user taps a button while a panel is animating closed, the close completes (or jumps to the end state) and the user's tap takes effect. Animations must not block input.

This rules out two common failure modes: long page transitions that swallow taps, and modals that re-open mid-close because the close animation hadn't "released" yet.

### 6. Transform and opacity only

This rule already lives in the Performance Constraints section below, but it belongs here too: never animate `width`, `height`, `top`, `left`, `margin`, `padding`, or `border`. Use `transform` and `opacity`. Anything else triggers layout and creates jank.

### 7. Spring physics for natural-feeling interactions

For motions that follow user input — drag, pull-to-refresh, modal sheet snap, tab transitions on touch — prefer spring physics over fixed-duration cubic-bezier curves.

Springs feel more natural because their deceleration matches how the user expects matter to behave when released. Fixed cubic-bezier easing is correct for state-based transitions that don't track gesture velocity.

---

## Reduced Motion

Reduced motion is documented under Motion Contracts above. The implementation pattern, repeated here for clarity:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0ms !important;
    scroll-behavior: auto !important;
  }
}
```

A blanket reset like this is the floor. It guarantees that no future component slips through. Component-level overrides may set `transition: none` or use a hook like `useReducedMotion()` to skip an animation entirely; both are acceptable, but the global reset must remain in place as a safety net.

The visual end state must still arrive — reduced motion suppresses the animation, not the outcome.

---

## Hover States

### Buttons

```css
.button--primary:hover {
  background-color: var(--color-action-primary-hover);
  transition: background-color var(--duration-normal) var(--ease-default);
}

.button--secondary:hover {
  background-color: var(--color-action-secondary-hover-bg);
  color: var(--color-action-secondary-hover-text);
  transition: background-color var(--duration-normal) var(--ease-default),
              color var(--duration-normal) var(--ease-default);
}
```

### Links

Standalone text links may reveal or strengthen underline on hover.
Inline prose links are governed separately in `prose.md` and remain underlined by default.
Navigation links usually shift color without adding hover underline.

```css
.link-standalone {
  text-decoration: none;
  transition: opacity var(--duration-fast) var(--ease-default);
}

.link-standalone:hover {
  text-decoration: underline;
  text-underline-offset: 0.2em;
}

.link-nav:hover {
  color: var(--color-link-nav-hover);
}
```

### Cards (if clickable)

Border color shift only. No transform, no shadow.

```css
.card-link:hover {
  border-color: var(--color-border-strong);
  transition: border-color var(--duration-normal) var(--ease-default);
}
```

### Trust Logos

Opacity shift.

```css
.trust-logo {
  opacity: 0.6;
  transition: opacity var(--duration-normal) var(--ease-default);
}

.trust-logo:hover {
  opacity: 0.9;
}
```

---

## Focus States

All interactive elements must have visible focus states for keyboard accessibility.

```css
:focus-visible {
  outline: 2px solid var(--color-focus-ring);
  outline-offset: 2px;
  transition: outline-offset var(--duration-fast) var(--ease-default);
}
```

On dark backgrounds:
```css
.dark-section :focus-visible {
  outline-color: var(--color-focus-ring-on-dark);
}
```

Rules:
1. **Never remove focus outlines.** `outline: none` is prohibited unless a custom focus indicator replaces it.
2. Focus states use the dedicated focus tokens on light and dark backgrounds. No accent colors for focus.
3. Use `:focus-visible` (not `:focus`) so mouse users don't see focus rings on click.

---

## Scroll-Triggered Entrances

Content sections may gently fade in as they enter the viewport. This is the only scroll-based animation allowed.

### The Single Entrance Pattern

```css
.section-reveal {
  opacity: 0;
  transform: translateY(16px);
  transition: opacity var(--duration-entrance) var(--ease-out),
              transform var(--duration-entrance) var(--ease-out);
}

.section-reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}
```

Triggered via `IntersectionObserver` when the section enters the viewport at approximately 15–20% visibility.

### Entrance Rules

1. **Fade + subtle upward translate only.** No horizontal slides, no scale, no rotation, no blur.
2. **16px translate maximum.** The movement is barely perceptible — it just prevents the content from appearing to "snap" into place.
3. **Each section animates as a single unit.** Do not stagger individual elements within a section (no "first the headline, then the body, then the image"). The entire section fades in together.
4. **Respect `prefers-reduced-motion`.** If the user has requested reduced motion, all scroll-triggered animations are disabled and content appears immediately.

```css
@media (prefers-reduced-motion: reduce) {
  .section-reveal {
    opacity: 1;
    transform: none;
    transition: none;
  }
}
```

5. **Hero section does not use entrance animation.** The hero is visible on page load — no fade-in delay.
6. **Maximum 8 animated sections per page.** If a page has more sections, the later ones should appear without animation to avoid the "everything slides in" fatigue.

---

## Accordion / Expand-Collapse

For FAQ sections or expandable content (used sparingly — see `components.md`).

```css
details[open] summary + .content {
  animation: accordion-open var(--duration-slow) var(--ease-in-out);
}

@keyframes accordion-open {
  from {
    opacity: 0;
    max-height: 0;
  }
  to {
    opacity: 1;
    max-height: 500px; /* arbitrary max — content determines actual height */
  }
}
```

Use native `<details>` / `<summary>` elements. The CSS handles the animation. No JavaScript accordion libraries.

---

## Nav Scroll Behavior

The header nav transitions from transparent (over the hero) to a solid background as the user scrolls past the hero section.

```css
.header {
  background-color: transparent;
  transition: background-color var(--duration-normal) var(--ease-default);
}

.header.is-scrolled {
  background-color: var(--color-bg-page);
  border-bottom: 1px solid var(--color-border-default);
}
```

Triggered via `IntersectionObserver` on the hero section — when the hero exits the viewport, the `.is-scrolled` class is applied.

---

## What We Do NOT Animate

1. **No parallax scrolling.** Background images do not move at different rates than content.
2. **No scroll-jacking.** The browser's native scroll behavior is never overridden.
3. **No animated counters.** Stat numbers display at their final value immediately.
4. **No loading spinners or skeleton screens** on initial page load. If content loads fast (and it will — no render-blocking JS), there's nothing to skeleton.
5. **No hover transforms on cards** (no scale-up, no lift, no shadow-on-hover).
6. **No animated backgrounds.** No gradient shifts, no particle effects, no moving textures.
7. **No page transition animations.** Pages load normally. No full-page fades or slides between routes.
8. **No auto-playing video in the hero.** If video is used, it requires user interaction to play.
9. **No text animation** (no typewriter effects, no character-by-character reveals, no word-by-word fades).
10. **No infinite scroll.** Pagination or "load more" buttons for content lists.

---

## Performance Constraints

1. All animations use `opacity` and `transform` only — these are GPU-composited and do not trigger layout recalculation.
2. Never animate `width`, `height`, `margin`, `padding`, `top`, `left`, or `border`. These trigger layout and are expensive.
3. All `IntersectionObserver` instances are created once and reused. No per-element observers.
4. The `will-change` property is applied only to elements currently animating, and removed after the animation completes. Never apply `will-change` globally.
