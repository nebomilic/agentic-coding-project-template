# Applications

Each folder here is one independently deployable application. An app may be a
user interface, a service, a scheduled job, or anything else that ships and
runs on its own.

## Rules

- **An app owns its own runtime concerns**: setup, configuration, tests,
  deployment entry point. Its README is the authority on how to run it.
- **Apps do not import from each other.** Shared code moves to `packages/`.
  If two apps need the same logic, that is the signal — not a reason to reach
  across the boundary.
- **Apps may depend on `packages/`**, never the reverse.
- **Adding an app is an architectural decision** and needs an ADR. Adding one
  is cheap; the coordination cost it creates is not.

## Each app folder contains

- `README.md` — what it is, how to run it, how it fits into the product
- `AGENTS.md` — constraints and conventions for agents working inside it
- its own source, tests, and configuration

The two apps scaffolded here, `web` and `api`, are illustrative. Rename,
remove, or add as the product requires.
