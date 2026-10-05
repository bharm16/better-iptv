# First TV build — approved ticket breakdown

Approved by the user on 2026-10-04 and refined on 2026-10-05 from the supplied architecture review. These are local Markdown tickets, not GitHub issue numbers. Acceptance criteria live in each individual ticket, with shared behavior in the [interaction contract](interaction-contract.md).

## Approved slices

1. **[Play a test channel in an installable TV build](issues/01-play-test-channel.md)** — **Blocked by:** None. **Delivers:** Launch an internal Android TV app, choose a clearly identified test channel, watch it full-screen, and return using the remote.
2. **[Connect a provider and watch its channels without guide data](issues/02-connect-provider.md)** — **Blocked by:** 01. **Delivers:** Enter a provider's Xtream Codes details on the TV, save the connection, browse its channels, and select one to watch even when no program listings exist.
3. **[Keep favorite channels in Home and the Guide](issues/03-favorite-channels.md)** — **Blocked by:** 02. **Delivers:** Favorite or unfavorite a channel with the remote and find the same saved choices in Home and the Guide after restarting.
4. **[Return to recently watched channels](issues/04-recent-channels.md)** — **Blocked by:** 02. **Delivers:** Find channels that actually played in a persistent Recents list on Home and the Guide and return to their current live broadcast.
5. **[Browse groups and search channel names](issues/05-browse-groups-and-search.md)** — **Blocked by:** 02. **Delivers:** Navigate the provider's groups or search channel names to find and play a channel without relying on program metadata.
6. **[Recover channel starts and interrupted playback](issues/06-recover-channel-starts.md)** — **Blocked by:** 02. **Delivers:** Finite initial/channel-switch and ongoing-playback recovery with distinct failure/ended states, explicit cancellation and responsive navigation.
7. **[Switch saved providers without mixing personal channels](issues/07-switch-providers.md)** — **Blocked by:** 03, 04, 05. **Delivers:** Save more than one provider and switch between their separate lineups, groups, favorites, recents, and search context.
8. **[Browse channels over full-screen playback](issues/08-browse-while-watching.md)** — **Blocked by:** 03, 04. **Delivers:** Open a compact channel browser while a channel remains full-screen, inspect favorites and recents, and switch only after an explicit selection.
9. **[Keep playback in a mini player and restore browsing context](issues/09-mini-player-and-return.md)** — **Blocked by:** 06, 07, 08. **Delivers:** Shared playback/recovery across full-screen and mini surfaces, latest-origin focus restoration, explicit Back/Stop and suspension/return behavior.
10. **[Hide and restore groups and channels](issues/10-hide-and-restore-channels.md)** — **Blocked by:** 09. **Delivers:** Remove unwanted groups or channels from ordinary browsing, then restore them without losing favorites, recents, or other saved choices.
11. **[Reorder groups and channels with the remote](issues/11-reorder-channel-lineup.md)** — **Blocked by:** 09. **Delivers:** Arrange channel groups and channels into a useful personal order and keep that order after restarting or refreshing the provider.
12. **[Expose supported playback and track controls](issues/12-supported-playback-controls.md)** — **Blocked by:** 09. **Delivers:** Use the active stream's supported pause, seek, audio, and subtitle controls consistently in full-screen and mini-player viewing.
13. **[Add optional program information without blocking channel access](issues/13-optional-program-information.md)** — **Blocked by:** 09. **Delivers:** See useful current-program information and a separate details action when the provider supplies it, while every channel remains usable without it.
14. **[Qualify the complete viewing loop on Google TV](issues/14-qualify-google-tv-build.md)** — **Blocked by:** 10, 11, 12, 13. **Delivers:** Produce the first installable test build with reproducible checks and evidence that the agreed setup-to-watch-to-return flow works on the user's Google TV, including recovery, Stop and lifecycle transitions.

## Scope

This batch covers the first native TV build. The full public-release plan remains in the [product spec](../product-discovery/spec.md). Each ticket contains its own behavior checks; the final qualification ticket joins the completed viewing loop.

All tickets are marked ready-for-agent. Readiness does not remove their blocking edges: work can begin only once the listed blockers are resolved. No ticket has been implemented or resolved by this documentation pass.
