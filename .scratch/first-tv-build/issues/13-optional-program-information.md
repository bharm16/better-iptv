# 13 — Add optional program information without blocking channel access

**What to build:** See useful current-program information and a separate details action when the provider supplies it, while every channel remains usable without it.

**Blocked by:** 09 — Keep playback in a mini player and restore browsing context

**Status:** ready-for-agent

**Type:** task

- [ ] Valid provider program information is shown as optional context in Home, Guide, channel browsing, and the active-player presentation where appropriate.
- [ ] Missing, malformed, stale, or slow guide data never blocks channel selection, tuning, or access to favorites and recents.
- [ ] Unavailable information is represented honestly; titles, progress, times, and artwork are not fabricated.
- [ ] A separate Details action is reachable from Channel actions and player controls without tuning; Back dismisses that top layer and restores the item/trigger or enabled fallback, preserving direct watch-live selection on channel/current-program items.
- [ ] Freshness rules and missing/invalid/stale copy are documented and tested within the first build; information known to be stale is not labeled as current or rendered with a current progress bar.
- [ ] Refreshing metadata does not unexpectedly move focus, reorder personal lists, or retune playback.
- [ ] Tests cover useful listings, empty data, invalid times/text, delayed responses, and continued channel playback; schedule-grid and archived-program browsing remain later scope.
