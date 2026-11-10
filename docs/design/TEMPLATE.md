# DESIGN-<NNNN>: <Title>

- **Status:** Current | Superseded by [DESIGN-<NNNN>](NNNN-<slug>.md) | Retired
- **Owner:** <Designer>
- **Updated:** <YYYY-MM-DD>
- **Related:** <PRDs, ADRs, other design entries>

## Reference

**Design:** [<frame or flow name>](<link>)
**Frame:** `<page / frame path as it appears in the file>`
**Linked:** <YYYY-MM-DD> · **Version:** <named version at handoff, not HEAD>
**State at link time:** <one line describing what the design actually showed —
the step count, the key elements, the notable choice>

That last line is the point of this block. A link resolves even after the
design has moved on; it just shows something other than what was built, with
nothing to signal the difference. The description is what lets a reader notice
the drift at the moment they would otherwise act on it.

Link to a named version wherever the design is settled. HEAD is for designs
still in motion, and should be re-pointed at a version once they are not.

## What this covers

<Which screens, flows or surfaces. Be specific about the edges — what a reader
might assume is included and is not.>

## Decisions

<The choices a mockup cannot carry on its own: why this pattern rather than the
obvious alternative, what varies by context, what must not be changed without
coming back here.>

## States

<Only where this entry departs from the defaults in DESIGN-0001. Otherwise say
so and leave the baseline to do its job.>

| State | Behaviour |
|---|---|
| <…> | <…> |

## Implementation notes

<Constraints the implementation must respect, and anything agreed after the
design was handed over. Record changes here rather than silently in the design
file, so the written record and the visual one stay in step.>

## Open questions

| Question | Who decides | By when |
|---|---|---|
| <…> | <…> | <…> |
