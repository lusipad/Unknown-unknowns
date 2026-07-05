# Unknowns-First Implementation Plan

A plan's job is not to list steps — it's to put the user's review time where decisions
might actually flip. Lead with what they're most likely to tweak; bury what they'd
rubber-stamp.

Fold in whatever this kickoff produced: criteria list, decision log, blindspot briefing,
semantics checklist.

## Write the plan in this exact order

### 1. Decisions you'll most likely tweak (top of the document)

Data model changes, new type interfaces, API shapes, anything user-facing. For each:

- The decision, concretely (show the actual schema / interface / flow, not a description)
- **Confidence: high / medium / low**
- **What would flip it** — the specific evidence or answer that would change the decision

This section is the review surface. Readable in five minutes.

### 2. Assumptions

Everything taken as given, each with confidence and source (user said it / found in
code / industry default). Industry-default assumptions get flagged loudest — they're the
ones most likely to be wrong for this codebase.

### 3. Deviation policy

Pre-authorize the implementer:

- **When an edge case forces a deviation: pick the conservative option, log it, keep
  going.** Define "conservative" for this task explicitly.
- List what must **stop and ask** instead: destructive migrations, security surface,
  anything that invalidates the plan's premise.

### 4. Mechanical work (bottom)

Refactoring, plumbing, boilerplate. One line each. Mark the section "low review value —
trust the implementer."

### 5. Verification

How we'll know it works: the observable behavior to demo, not just "tests pass."

## Review loop

Walk the user through **section 1 only**. Adjust until they stop tweaking. Don't burn
their attention on the mechanical section.

## Handoff

Recommend executing in a **fresh session**: pass the plan plus any artifacts, and
include the implementation-notes setup (see `impl-notes.md`) in the handoff instructions
so deviations get logged instead of silently improvised. What the implementation learns
becomes the map for next time.
