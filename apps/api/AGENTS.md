# Agent instructions — API service

Inherits the root `AGENTS.md`. Rules below take precedence within this folder.

## Boundaries

- This service owns its data store. No other app connects to it. If another
  app needs the data, it needs an interface, not a connection string.
- The public interface is a contract. Changing it in a way that breaks existing
  clients requires an ADR and a migration path — never a silent change.
- Do not add a new external dependency or third-party service without an ADR.
  Each one is a long-term operational commitment.

## Non-negotiables

- **Validate every input at the boundary.** Never trust a client, including our
  own.
- **Enforce authorisation per request**, on the server, close to the data. Do
  not rely on a client having hidden an action.
- **Never log credentials, tokens, or personal data.** When in doubt, log an
  identifier instead of a value.
- **Every schema change ships with a migration** that can be applied to an
  existing environment and, where feasible, reversed.
- **Errors are typed and deliberate.** Internal failure details do not reach
  the client; they reach the logs.

## Conventions

- <Module and layering conventions.>
- <Error handling and response shape.>
- <Logging and observability expectations.>

## Definition of done, this service

In addition to the root checklist:

1. Build passes and the test suite is green.
2. New or changed behaviour is covered through the service's public interface,
   including the failure paths: rejected input, missing authorisation, and the
   dependency being unavailable. Authorisation in particular is tested as a
   denial, not only as a success.
3. Any interface change is reflected in the contract and flagged to clients.
4. Any schema change has a migration.
5. No secrets or personal data in logs, fixtures, or examples.
