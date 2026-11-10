# ADR-0004: Research findings in the repository, evidence outside it

- **Status:** Accepted
- **Date:** 2026-11-10
- **Deciders:** <names>
- **Related:** [ADR-0001](./0001-record-architecture-decisions.md),
  [ADR-0003](./0003-work-tracking.md)

## Context

Product decisions should rest on something. A PRD asserting "users struggle
with X" is weaker than one that traces the claim to research, and an agent
drafting a PRD with no access to evidence will invent plausible user needs —
it is very good at that, which is the problem.

That argues for research being present in the repository. The question is what
"present" should mean, because research arrives as two quite different things:
curated findings, and the raw material behind them — interview transcripts,
recordings, survey exports, purchased analyst reports.

The repository is well suited to the first and badly suited to the second.

## Decision

Findings live in `docs/research/`. Raw evidence does not enter the repository.

1. **A finding is a curated claim**: one sentence, with its method, sample,
   confidence, and a pointer to where the evidence lives. It is short enough to
   review in a diff and useful to someone reading it two years later.
2. **Raw evidence stays in the system that holds it** — the team's drive, the
   research tool, wherever the recordings already are. Each note records the
   location and who grants access, so the chain from claim to source survives
   without the source being here.
3. **Personal data does not enter the repository at all.** No transcripts, no
   recordings, no participant names, employers, or identifying detail. Quotes
   appear only anonymised and only where they carry analytical weight.
4. **Findings carry two dates** — as of, and revisit by. They are perishable in
   a way nothing else here is.
5. **Licensed material is referenced, never reproduced.** A purchased report
   usually may not be redistributed, and a repository clone is redistribution.

## Alternatives considered

| Option | Why not |
|---|---|
| Raw transcripts committed alongside findings | Unreviewable in a diff, dilutes retrieval, and carries personal data into permanent history |
| Findings in the issue tracker instead | Same failure as tickets holding knowledge ([ADR-0003](./0003-work-tracking.md)): written once, never curated, invisible to agents |
| No research folder; cite sources inline in PRDs | Every PRD re-states the same finding, each drifting separately, with no single place to correct it |
| Keep everything in the research tool, nothing here | Findings stop being ambient context, and PRDs go back to asserting user needs from nowhere |

## Consequences

**What this makes easier**

- PRDs can be grounded in a citable claim with a stated confidence level.
- Agents get the finding without the transcript, which is the useful half.
- Participants' data stays in a system where access can be revoked and
  deletion actually deletes.

**What this makes harder, or commits us to**

- Someone must do the curation. A finding does not write itself from a
  transcript, and the discipline is the cost of the benefit.
- Two systems to keep in step, with the pointer always running from the
  repository outward.
- Findings decay silently unless the index is reviewed each planning cycle.
  Nothing enforces this; it is a habit or it does not happen.

**User-visible effects** — none directly. The people whose data this protects
are research participants rather than product users, and the protection is the
point.

## Why the personal-data rule is not a tradeoff

The property that makes version control right for decisions — immutable,
distributed history — is exactly what makes it wrong for personal data. A
transcript committed once exists in every clone, permanently; removing it means
rewriting history across every copy that was ever taken. Under the GDPR, a
deletion request against a distributed repository history is close to
unanswerable.

Participants consented to research. They did not consent to sitting in a
repository that every contractor clones. That is a line rather than a cost to
weigh, and it does not move for convenience.

## Revisit when

Findings are routinely written and never read, which would mean the curation
cost is buying nothing. Or the pointer to raw evidence stops resolving for most
notes, which would mean the chain is broken and the findings are now
unverifiable assertions.
