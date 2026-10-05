# 11 — Reorder groups and channels with the remote

**What to build:** Arrange channel groups and channels into a useful personal order and keep that order after restarting or refreshing the provider.

**Blocked by:** 09 — Keep playback in a mini player and restore browsing context

**Status:** ready-for-agent

**Type:** task

- [ ] Guide → Organize → Groups/Channels → Move enters a visible draft move mode; the D-pad moves the item, Finish commits, and Cancel/Back discards the draft without needing touch or drag gestures.
- [ ] Provider-scoped group/channel order is projected into Guide, All/Ungrouped, Favorites, favorite-browser sections and channel-name search; Recents and recent-browser sections remain chronological.
- [ ] Cancel leaves the saved order unchanged; confirmed changes survive app restart and provider refresh.
- [ ] New groups/channels append in provider order without resetting saved order; stable removed identities do not corrupt surviving positions.
- [ ] Catalog updates are queued during a draft move and reconciled after Finish/Cancel. If the moving item disappears, discard that draft with feedback and restore a surviving item/control; never reshuffle items underneath active move focus.
- [ ] Reordering keeps a meaningful focused item and does not alter or interrupt the active stream.
- [ ] Tests cover moves, cancellation, refresh additions/removals, persistence, and provider separation.
