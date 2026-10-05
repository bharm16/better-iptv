# First TV build map

## Notes

The user approved this 14-ticket breakdown on 2026-10-04. The supplied architecture review subsequently refined the behavior and added ongoing recovery and Stop. The configured tracker is one local Markdown file per ticket; implementation and acceptance are still unperformed.

Read the [first-build scope](spec.md), [interaction contract](interaction-contract.md), [domain glossary](../../CONTEXT.md), and relevant [ADRs](../../docs/adr/) before implementation. The [UX architecture board](https://www.figma.com/board/JluDgNpnfYoTbMeOkq5mE7) presents the same behavior. Ticket numbers below belong to this feature and are not GitHub issue identifiers.

## Decisions-so-far

The [approved breakdown](ticket-breakdown.md) follows the complete viewing path through a working TV build, provider access, local personalization, playback presentation, and qualification. Every ticket includes acceptance checks.

| Ticket | Blocked by | State |
| --- | --- | --- |
| [01 — Play a test channel in an installable TV build](issues/01-play-test-channel.md) | None | ready-for-agent |
| [02 — Connect a provider and watch its channels without guide data](issues/02-connect-provider.md) | 01 | ready-for-agent |
| [03 — Keep favorite channels in Home and the Guide](issues/03-favorite-channels.md) | 02 | ready-for-agent |
| [04 — Return to recently watched channels](issues/04-recent-channels.md) | 02 | ready-for-agent |
| [05 — Browse groups and search channel names](issues/05-browse-groups-and-search.md) | 02 | ready-for-agent |
| [06 — Recover channel starts and interrupted playback](issues/06-recover-channel-starts.md) | 02 | ready-for-agent |
| [07 — Switch saved providers without mixing personal channels](issues/07-switch-providers.md) | 03, 04, 05 | ready-for-agent |
| [08 — Browse channels over full-screen playback](issues/08-browse-while-watching.md) | 03, 04 | ready-for-agent |
| [09 — Keep playback in a mini player and restore browsing context](issues/09-mini-player-and-return.md) | 06, 07, 08 | ready-for-agent |
| [10 — Hide and restore groups and channels](issues/10-hide-and-restore-channels.md) | 09 | ready-for-agent |
| [11 — Reorder groups and channels with the remote](issues/11-reorder-channel-lineup.md) | 09 | ready-for-agent |
| [12 — Expose supported playback and track controls](issues/12-supported-playback-controls.md) | 09 | ready-for-agent |
| [13 — Add optional program information without blocking channel access](issues/13-optional-program-information.md) | 09 | ready-for-agent |
| [14 — Qualify the complete viewing loop on Google TV](issues/14-qualify-google-tv-build.md) | 10, 11, 12, 13 | ready-for-agent |

The initial dependency frontier is **01**. Once **02** is resolved, **03**, **04**, **05**, and **06** can proceed independently. The individual ticket files are authoritative for blockers and execution status.

The review adds **06 → 09** for shared recovery integration in the mini player; **06 → 14** is now transitive through 09 and its dependents. No new ticket or implementation completion is implied.

## Fog

- Implementation and all acceptance checks remain unperformed.
- Numeric recovery budgets/classification, program-information freshness/copy and physical remote mapping remain first-build decisions to resolve and validate; they are not later-release exclusions.
- Native device qualification needs the actual TV model/OS, installation setup, and representative streams; no compatibility claims are implied by ticket publication.
- The later public-release work remains in the product spec: phone setup service, trial/purchase integration, schedule grid, and release preparation. This batch does not mark any of those complete.
