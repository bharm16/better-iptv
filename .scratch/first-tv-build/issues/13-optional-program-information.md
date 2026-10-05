# 13 — Add optional program information without blocking channel access

**What to build:** See useful current-program information and a separate details action when the provider supplies it, while every channel remains usable without it.

**Blocked by:** 09 — Keep playback in a mini player and restore browsing context

**Status:** ready-for-agent

**Type:** task

- [ ] Valid provider program information is shown as optional context in Home, Guide, channel browsing, and the active-player presentation where appropriate.
- [ ] Missing, malformed, stale, or slow guide data never blocks channel selection, tuning, or access to favorites and recents.
- [ ] Unavailable information is represented honestly; titles, progress, times, and artwork are not fabricated.
- [ ] A separate details action preserves the one-selection path from a channel/current-program item to live playback.
- [ ] Refreshing metadata does not unexpectedly move focus, reorder personal lists, or retune playback.
- [ ] Tests cover useful listings, empty data, invalid times/text, delayed responses, and continued channel playback; schedule-grid and archived-program browsing remain later scope.
