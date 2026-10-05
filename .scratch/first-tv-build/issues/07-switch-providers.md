# 07 — Switch saved providers without mixing personal channels

**What to build:** Save more than one provider and switch between their separate lineups, groups, favorites, recents, and search context.

**Blocked by:** 03 — Keep favorite channels in Home and the Guide; 04 — Return to recently watched channels; 05 — Browse groups and search channel names

**Status:** ready-for-agent

**Type:** task

- [ ] Multiple saved connections can be added and selected; the chosen provider is clear in Home and the Guide.
- [ ] Selection changes the browsing catalog without merging lineups or automatically choosing a stream.
- [ ] Global Guide restores the last browsed provider's collection, query and focus. A provider-scoped All channels action explicitly names and opens that provider without tuning; cross-player navigation is integrated in ticket 09.
- [ ] Favorites, recents, groups, search state, and channel identity remain associated with the correct provider, including identical channel IDs/names in different providers.
- [ ] The selected provider is restored after restarting; an unavailable provider does not prevent choosing another saved connection.
- [ ] Late catalog responses from a previously selected provider cannot overwrite the current provider's visible state.
- [ ] End-to-end coverage switches between two controlled providers before and after restart and verifies personal-data isolation.
