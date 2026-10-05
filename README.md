# Better IPTV

A live IPTV player planned for Google/Android TV, followed by Android-based Fire OS devices.

The repository currently contains the product specification, research, architectural decisions, and first-build planning. App implementation has not started.

## Product direction

- Bring an existing Xtream Codes provider connection.
- Find familiar channels through favorites and recents in Home and the Guide.
- Keep channel browsing and playback useful when program-guide information is missing.
- Browse over full-screen playback or continue watching in a mini player.
- Retain personal channel choices on the device across restarts.
- Use Kotlin, Compose for TV, and Media3 for the initial app.

## Planning documents

- [Product scope and decisions](.scratch/product-discovery/spec.md)
- [Discovery map](.scratch/product-discovery/map.md)
- [First native TV build](.scratch/first-tv-build/spec.md)
- [First-build tickets and dependencies](.scratch/first-tv-build/map.md)
- [Approved ticket breakdown](.scratch/first-tv-build/ticket-breakdown.md)
- [Domain glossary](CONTEXT.md)
- [Architecture decisions](docs/adr/)
- [Stack research](.scratch/product-discovery/research-stack.md)
- [TV UX research](.scratch/product-discovery/research-tv-ux.md)

The configured issue tracker uses one local Markdown file per ticket. The first build has 14 approved tickets with explicit blocking edges and acceptance criteria.
