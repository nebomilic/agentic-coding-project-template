# ADR-0002: Testing strategy

- **Status:** Accepted
- **Date:** 2026-11-09
- **Deciders:** <names>
- **Related:** [ADR-0001](./0001-record-architecture-decisions.md)

## Context

"Write tests" is not an instruction anyone can follow consistently. Without a
stated layer rule, each contributor picks a different one, and the suite drifts
towards whichever layer is easiest to write rather than whichever layer catches
real defects.

AI coding agents make this concrete. Told only that tests must exist, an agent
reliably produces a heavily mocked unit test that asserts the implementation
back to itself: it passes, it covers the lines, and it will keep passing after
the behaviour breaks. That test is worse than no test, because it buys
confidence that is not there.

The repository also has no home for testing that is not automated — release
acceptance, exploratory passes, the judgement calls a machine reads poorly —
and no statement of who owns the criteria those checks are measured against.

## Decision

We will test by observable behaviour at the lowest layer that can observe it
honestly, and record that rule where agents and contributors read it.

1. **Tests live with the code they test.** No central test folder. An app or
   package owns its own suite, in its own structure.
2. **Test through the public interface.** A test that reaches into internals
   couples the suite to the implementation and blocks the refactors tests are
   supposed to enable.
3. **Choose the lowest honest layer.** Prefer a unit test when the behaviour is
   genuinely local. Use an integration test when the behaviour only exists in
   the interaction — a query, a transaction, a request path. Pushing everything
   down produces fast suites that prove nothing; pushing everything up produces
   slow suites nobody runs.
4. **Mock only at boundaries we do not own** — third-party services, the clock,
   the network. Mocking our own modules is how a test ends up asserting the code
   it is testing.
5. **Cross-app flows are tested end-to-end, sparingly.** A small set covering
   the paths that would be severe if broken. End-to-end tests are the most
   expensive to write, slowest to run and most prone to flaking; they earn their
   place by covering what no narrower test can.
6. **Manual testing is reserved for what automation reads poorly**: visual and
   interaction judgement, exploratory passes against new surfaces, first-run and
   setup paths, and accessibility checks that need a real assistive technology.
   It is a deliberate choice per case, not the residue of what nobody automated.
7. **Acceptance criteria originate in the PRD.** The Product Manager writes
   them as success criteria; automated and manual checks both derive from there.
   A check nobody can trace back to a stated requirement is a check nobody can
   argue with when it fails.
8. **No global coverage target.** Coverage is read as a diagnostic — an
   untested path worth asking about — never as a gate. A percentage target is
   satisfied most cheaply by tests that assert nothing.

## Alternatives considered

| Option | Why not |
|---|---|
| A top-level `tests/` folder | Tests drift from the code they cover, ownership blurs, and it contradicts an app owning its own runtime concerns |
| A coverage percentage gate in CI | Measures execution, not verification; reliably met by assertion-free tests |
| Mandating the test pyramid by ratio | A ratio is an outcome of good layer choices, not an input to them |
| Testing primarily end-to-end | Slow, flaky, and poor at localising a failure — the suite stops being run |
| Leaving the rule unstated | The status quo that produced inconsistent suites and self-asserting agent tests |

## Consequences

**What this makes easier**

- Agents have a layer rule to apply instead of a gap to fill with a guess.
- Refactoring stays possible, because tests are coupled to behaviour rather
  than structure.
- Manual effort goes where it is actually better than a machine.
- A failing acceptance check traces back to a written requirement and an owner.

**What this makes harder, or commits us to**

- Judgement is required per test, which is slower than following a ratio and
  harder to enforce mechanically. Review has to carry that weight.
- Without a coverage gate, gaps are found by people reading diffs, not by CI.
- Integration tests need real dependencies available locally and in CI, which
  is setup cost paid up front.

**User-visible effects** — none directly. Indirectly, defects that reach users
are more likely to be ones no reasonable test would have caught.

## Revisit when

A class of defect reaches users repeatedly despite a green suite — that is
evidence the layer rule is wrong somewhere, and the pattern of escapes will say
where. Also revisit if end-to-end flakiness starts causing green builds to be
ignored, which destroys the value of every layer beneath it.
