# Issue tracker: Local Markdown

Issues and specs live as Markdown files in `.scratch/`.

## Conventions

- One feature per directory: `.scratch/<feature-slug>/`.
- Spec: `.scratch/<feature-slug>/spec.md`.
- Tickets: `.scratch/<feature-slug>/issues/<NN>-<slug>.md`,
  numbered from `01`, with one file per ticket.
- Record triage state in a `Status:` line near the top,
  using the roles in `triage-labels.md`.
- Append conversation under `## Comments`.

## Publishing and fetching

When a skill says "publish to the issue tracker", create the appropriate
spec or ticket file under `.scratch/<feature-slug>/`.

When a skill says "fetch the relevant ticket", read the referenced file.
Resolve ticket numbers within the referenced feature directory.

## Wayfinding operations

- Map: `.scratch/<effort>/map.md`, containing Notes,
  Decisions-so-far, and Fog.
- Child tickets: `.scratch/<effort>/issues/NN-<slug>.md`.
- Record ticket type in `Type:`:
  `research`, `prototype`, `grilling`, or `task`.
- Record dependencies in `Blocked by: NN, NN`.
- An unblocked ticket has every listed dependency resolved.
- Select the first open, unblocked, unclaimed ticket by number.
- Claim by saving `Status: claimed` before starting work.
- Resolve by appending `## Answer`, setting `Status: resolved`,
  and adding a gist and ticket link to the map's Decisions-so-far.
