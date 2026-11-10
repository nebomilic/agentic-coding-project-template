# Design

Visual and interaction decisions that apply beyond a single screen. Owned by
the Designer.

## Index

| # | Title | Status | Updated |
|---|---|---|---|
| [0001](0001-design-foundations.md) | Design foundations | Current | <YYYY-MM-DD> |

## Source of truth

**The design tool remains canonical for visuals.** Nothing here tries to mirror
screen designs; that duplication would be stale within a sprint.

Canonical file: <link>

What lives here instead are the decisions that a mockup cannot carry:

- **Foundations** — the token system, and the reasoning behind its scales.
- **Rules that span screens** — state conventions, density, motion, hierarchy.
- **Accessibility baseline** — the standard we hold to and what that means in
  practice.
- **Component policy** — when to reuse, when to extend, when a new component is
  justified.
- **Which design file is canonical**, and what to do when it and the
  implementation disagree.

## Why these must be written down

A decision that exists only as a comment in a design file is invisible to a
developer six months from now and invisible to every coding agent working in
this repository. The implementation will drift from it, and the drift will only
surface when someone notices two screens disagree. Writing the rule down, and
encoding its values in `packages/shared/tokens/`, is what makes it enforceable.

## Per-feature entries

Foundations are not the only thing that belongs here. A feature's designs get
their own numbered entry, from `TEMPLATE.md`, whenever they establish a pattern
others will follow. A genuine one-off screen does not need one — its PRD can
carry the reference directly.

The entry exists so the link has an owner and a single home. A PRD points at
the entry; the entry points at the design file. When the design moves, one
document changes rather than every PRD that mentioned it, and the Designer
maintains the pointer to their own work rather than the Product Manager
maintaining a link to something they do not control.

## Referencing a design file

Never a bare URL. Every reference records what it pointed at:

```
**Design:** [Checkout flow — v2](<link>)
**Frame:** `Checkout / v2 / Desktop`
**Linked:** 2026-03-14 · **Version:** "v2 handoff"
**State at link time:** three-step flow, guest checkout on step 1
```

A design-tool URL points at mutable state. Frames get renamed, moved,
redesigned for the next feature, archived. The link keeps resolving — it just
stops showing what was meant, and nothing announces that. A stale link is worse
than a broken one, because a broken link admits it.

The last line carries the weight. Someone opening that reference later and
finding a four-step flow with no guest option knows immediately that the design
changed after the document was written. That is a question to raise, not a
detail to absorb silently.

Link to a **named version** at handoff rather than to the file's current state.
HEAD is for designs still moving, and should be re-pointed once they settle.

## What nothing here solves

No part of this setup notices when a design changes. The repository cannot
watch the design tool, and an issue tracker would not either unless someone
moved a ticket by hand. The design tool's own notifications reach whoever
subscribed, not whoever is about to implement from a stale reference.

The dated state description above is the only mechanism here that catches that
drift, and it catches it at read time rather than at change time. Weaker than a
notification — but it sits in the document where the mistake would otherwise be
made.

## Relationship to tokens

Documents here explain *why* the system is shaped as it is.
`packages/shared/tokens/` holds the values themselves, and is what the code
consumes. When the two disagree, the tokens are what ships — so a change to the
reasoning is incomplete until the tokens follow.
