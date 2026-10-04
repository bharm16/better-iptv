# Domain Docs

## Before exploring

Read root `CONTEXT.md` and ADRs in `docs/adr/` relevant to the work.

If a root `CONTEXT-MAP.md` exists, follow its pointers and read the
contexts relevant to the topic, including their scoped ADRs.

If these files are absent, proceed silently. Domain modeling creates
them lazily as terminology and decisions are resolved.

## Layout

This repo uses a single-context layout:

- `CONTEXT.md`: domain terminology at the repo root.
- `docs/adr/`: architectural decisions.

## Vocabulary

Use the terms defined in `CONTEXT.md` when naming domain concepts.
For a missing concept, reconsider whether it belongs to the domain;
record real terminology gaps for domain modeling.

## ADR conflicts

Explicitly flag proposals that contradict an existing ADR.
Identify the ADR and explain why its decision should be reconsidered.
