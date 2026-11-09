# Infrastructure

Definitions of the environments the product runs in, and how it gets there.

## What belongs here

- Environment definitions, expressed as code rather than as console clicks.
- Deployment pipeline configuration.
- Shared service and network configuration.
- Environment-specific configuration templates — **templates only, never
  secrets**.

## Principles

- **Environments are defined here, not configured by hand.** A change made
  directly in a console is invisible, unreviewable, and will be silently
  reverted by the next deployment.
- **Environments differ by configuration, not by structure.** If staging is
  shaped differently from production, staging is not testing production.
- **Secrets live in a secret store.** This folder holds the reference to a
  secret, never its value — including in examples and test fixtures.
- **Infrastructure changes need the same review as code**, and the ones that
  commit the project long-term need an ADR.

## Environments

| Environment | Purpose | Who deploys |
|---|---|---|
| <…> | <…> | <…> |

## Procedures

Deployment steps, rollback, and incident response live in `docs/runbooks/`.
This folder holds the definitions; the runbooks hold the actions.
