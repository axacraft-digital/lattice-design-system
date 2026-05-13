# AGENT.md

## Purpose

This repository is the source-of-truth specification for the Lattice design system.
It is documentation-first. There may be little or no runnable application code.

Codex should treat the Markdown files in this folder as operating rules, not inspiration.
If a proposed implementation, component, section, or token conflicts with these specs, the spec wins unless the user explicitly approves an exception.

---

## What This Repository Contains

- Design foundations:
  - `typography.md`
  - `spacing.md`
  - `grid.md`
  - `colors.md`
- Applied system rules:
  - `prose.md`
  - `components.md`
  - `buttons.md`
  - `forms.md`
  - `badges.md`
  - `icons.md`
  - `density.md`
  - `surfaces.md`
  - `links.md`
  - `states.md`
  - `motion.md`
  - `section-archetypes.md`

This repository does not define page-by-page compositions, merchant strategy, SEO structure, or implementation details outside the design-system layer.

---

## Source Of Truth Order

When answering questions, reviewing work, or generating implementation guidance, read and apply the specs in this order:

1. `README.md`
2. `SYSTEM-MAP.md`
3. `typography.md`
4. `spacing.md`
5. `grid.md`
6. `colors.md`
7. `prose.md`
8. `components.md`
9. `buttons.md`
10. `forms.md`
11. `badges.md`
12. `icons.md`
13. `density.md`
14. `surfaces.md`
15. `links.md`
16. `states.md`
17. `motion.md`
18. `section-archetypes.md`

If two decisions appear to conflict, prefer the earlier foundational file unless the later file is clearly defining a consumption rule that depends on it.

---

## Operating Rules For Codex

1. Do not invent local tokens when a system token already exists.
2. Do not introduce ad hoc spacing, color, or type rules inside components or sections.
3. Do not style components from primitive color tokens when semantic tokens exist.
4. Do not bypass the prose container for raw rich text or merchant-authored HTML.
5. Do not bypass reading measure for sustained copy.
6. Do not create a new section pattern before checking `section-archetypes.md`.
7. Do not create a new archetype unless the existing system genuinely cannot express the need.
8. Do not treat visual styling as independent from density, surfaces, states, and motion.
9. Do not flatten all UI into generic “components”; distinguish primitives, structured components, and patterns.
10. Do not make frontend decisions from taste alone. Trace them back to the relevant spec file.

---

## Design Intent To Preserve

Codex should preserve the system's overall character:

- restrained, warm, and clinically composed
- Swiss-influenced and editorial, not generic SaaS
- precise at the micro level and architectural at the macro level
- motion that is functional and quiet, never decorative
- square-cornered controls by default
- semantic tokens and governed roles over one-off styling

Avoid soft, bubbly, overly colorful, shadow-heavy, or trend-driven UI unless the user explicitly asks to depart from the system.

---

## How To Work In This Repo

When the user asks for design or implementation help:

1. Read `README.md` first.
2. Read `SYSTEM-MAP.md` next for the internal dependency model.
3. Read only the spec files relevant to the request, following the dependency order above.
4. Identify which foundation rules govern the request.
5. Map the request to existing semantic tokens, component roles, density modes, surface planes, and section archetypes before proposing anything new.
6. In responses, cite the specific files that justify the decision.

When the user asks for a new component or section:

1. Determine whether it is a primitive, a structured component, or a pattern.
2. Determine whether an existing section archetype already fits.
3. Specify:
   - the typography roles
   - spacing semantics
   - grid frame and allocation
   - surface choice
   - density mode
   - link family
   - button/control sizing
   - required states
   - motion behavior, if any

When reviewing code or designs:

1. Treat deviations from the documented system as findings.
2. Prioritize violations of foundational rules over surface-level styling comments.
3. Call out drift explicitly: local tokens, arbitrary spacing, raw palette usage, prose bypass, section-archetype bypass, or state/motion inconsistency.

---

## File Editing Guidance

If asked to update these docs:

- preserve the existing voice: direct, governed, and system-oriented
- keep additions rule-based rather than inspirational
- extend existing systems instead of adding disconnected exceptions
- update dependent files when a foundational rule changes

If asked to generate implementation code from these docs:

- consume semantic tokens rather than raw primitives wherever possible
- preserve the semantic/visual type split
- preserve the spacing behavior layers
- preserve reading width constraints for long-form text
- preserve the defined link families and shared state behavior

---

## Response Style

When working in this repository, Codex should be explicit about:

- which files were consulted
- which rule or dependency determined the recommendation
- whether a recommendation is a direct spec requirement or an inference from the specs

If the repository does not contain enough information to answer an implementation detail, say so plainly instead of inventing undocumented system behavior.
