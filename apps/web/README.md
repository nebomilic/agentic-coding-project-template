# Web — user-facing application

## What it is

The interface users interact with. <One paragraph: who uses it, what they come
here to do, and what it deliberately does not do.>

## How it fits

Talks to `api` over its public interface only. Consumes shared types, utilities
and design tokens from `packages/shared`. Holds no business rules of its own
that the API does not also enforce — anything the client can enforce, a
determined user can bypass.

## Running it locally

<Prerequisites.>

<Install step.>

<Run step.>

<How to point it at a local vs. shared API.>

## Configuration

| Variable | Purpose | Required |
|---|---|---|
| `<NAME>` | <what it controls> | yes / no |

Copy `.env.example` to `.env` and fill in the values. Never commit `.env`.

## Tests

<How to run the test suite, and what each layer covers.>

## Where things are decided

- Product behaviour → `docs/prd/`
- Technical choices → `docs/adr/`
- Visual and interaction rules → `docs/design/` and `packages/shared/tokens/`
