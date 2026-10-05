# 11 — Reorder groups and channels with the remote

**What to build:** Arrange channel groups and channels into a useful personal order and keep that order after restarting or refreshing the provider.

**Blocked by:** 09 — Keep playback in a mini player and restore browsing context

**Status:** ready-for-agent

**Type:** task

- [ ] Group and channel reordering can be performed without touch or drag-only gestures, with clear move, finish, and cancel behavior.
- [ ] Saved order is provider-scoped and consistently applied to relevant browsing lists; Recents retains its chronological meaning.
- [ ] Cancel leaves the saved order unchanged; confirmed changes survive app restart and provider refresh.
- [ ] New channels have a deterministic documented placement without resetting existing personal order, and removed channels do not corrupt remaining positions.
- [ ] Reordering keeps a meaningful focused item and does not alter or interrupt the active stream.
- [ ] Tests cover moves, cancellation, refresh additions/removals, persistence, and provider separation.
