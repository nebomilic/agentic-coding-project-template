# DESIGN-0001: Design foundations

- **Status:** Current
- **Owner:** <Designer>
- **Updated:** <YYYY-MM-DD>
- **Implemented in:** `packages/shared/tokens/`

> Worked example. Replace the placeholders with the real system.

## Principles

<Two or three statements that resolve arguments. Not adjectives — principles
that can be applied to a specific decision and produce an answer. "Density over
whitespace where users work daily" settles a layout debate; "clean and modern"
does not.>

## Token system

| Category | Scale | Rationale |
|---|---|---|
| Spacing | <the scale> | <why this scale, and why these steps> |
| Typography | <the scale> | <…> |
| Colour | <semantic roles, not raw names> | <…> |
| Radius | <…> | <…> |
| Elevation | <…> | <…> |
| Motion | <durations and easing> | <…> |

Colour tokens are named by **role**, not appearance — a token called
`surface-raised` survives a palette change; one called `light-grey` does not,
and will be wrong the first time a dark theme appears.

## Mandatory states

Every view handles four states. A view that handles only content is incomplete,
whether or not the ticket mentioned the rest.

| State | Convention |
|---|---|
| Loading | <…> |
| Empty | <…what it says, and what action it offers> |
| Error | <…what it says, and how recovery works> |
| Content | <…> |

## Accessibility baseline

- Target standard: <standard and level>
- Text contrast minimum: <ratio>
- Every interactive element is keyboard-reachable with a visible focus state.
- Meaning is never carried by colour alone.
- Interactive elements have accessible names.

This is a floor, not an aspiration. Work that does not meet it is not done.

## Component policy

- Reuse an existing component before creating a new one, even when the fit is
  imperfect. A near-duplicate with subtly different behaviour costs more than
  an imperfect reuse.
- Extend a component when the variation is a genuine variant of the same thing.
- Create a new component only when the behaviour is genuinely distinct — and
  record it here when it establishes a new pattern.

## When implementation and design disagree

<State the resolution process, and who decides. The common case is a design
that did not anticipate a real constraint; the second most common is an
implementation that quietly invented a value. Both need a named owner.>
