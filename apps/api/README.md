# API — backend service

## What it is

The service that holds the product's business rules and owns its data.
<One paragraph: what it is responsible for, and what it deliberately is not.>

## How it fits

Serves `apps/web` and any other client. It is the enforcement point for every
rule that matters — clients may duplicate checks for responsiveness, but this
service is the authority. It owns the data store; nothing else connects to it
directly.

## Running it locally

<Prerequisites.>

<Install step.>

<Data store setup and seeding.>

<Run step.>

## Configuration

| Variable | Purpose | Required |
|---|---|---|
| `<NAME>` | <what it controls> | yes / no |

Copy `.env.example` to `.env` and fill in the values. Never commit `.env`.

## Interface

<Where the interface contract lives and how it is kept current — generated,
hand-written, or both. State which one wins when they disagree.>

## Tests

<How to run them. What is covered where.>

## Operational procedures

See `docs/runbooks/` for deployment, incident response, and recurring tasks.
