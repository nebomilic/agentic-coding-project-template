# shared

Cross-cutting primitives used by more than one application: the vocabulary the
apps have in common.

## What belongs here

- **Design tokens** — colour, spacing, typography, radius, elevation, motion.
  The Designer owns the values; the Developer owns the format they ship in.
- **Shared types and contracts** describing data that crosses app boundaries.
- **Pure utilities** with no environment assumptions — formatting, validation
  rules, small transformations.
- **Shared constants** that would otherwise drift apart in two places.

## What does not belong here

- Anything used by exactly one app. It belongs in that app.
- Business logic. That belongs in the service that owns the rule.
- Anything that reads configuration, touches the network, or assumes a runtime.
- Anything placed here because no other folder felt right. That is the signal
  the structure needs a conversation, not a drawer.

## Structure

```
shared/
├── tokens/     design values — Designer-owned
├── types/      shared contracts
└── utils/      pure helpers
```

## Changing tokens

Token values are a design decision. Changing one is not a refactor — it
propagates to every surface at once. Changes require the Designer's approval
(enforced via `CODEOWNERS`) and a note in `docs/design/` when the change
reflects a shift in the system rather than a correction.
