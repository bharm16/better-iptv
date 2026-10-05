# 10 — Hide and restore groups and channels

**What to build:** Remove unwanted groups or channels from ordinary browsing, then restore them without losing favorites, recents, or other saved choices.

**Blocked by:** 09 — Keep playback in a mini player and restore browsing context

**Status:** ready-for-agent

**Type:** task

- [ ] Hide and unhide actions for groups and individual channels are usable with the remote and are stored for the selected provider.
- [ ] Hidden channels and channels in hidden groups are excluded from ordinary Home, Guide, search, and channel-browser lists.
- [ ] Guide → Organize → Manage hidden items exposes hidden items for restoration and remains reachable from empty ordinary views; hiding changes visibility rather than deleting provider data or saved favorite/history records.
- [ ] Restoring visibility brings eligible saved entries back without guessing identities; these preferences survive restart and catalog refresh.
- [ ] Hiding the currently playing channel does not retune or stop it; focus moves to a next/previous surviving item, then Manage hidden items when ordinary browsing is empty. Restore confirms success and returns focus to a surviving management item or Back to channels.
- [ ] Cross-view tests cover hide/restore, persistence, active playback, and isolation between providers.
