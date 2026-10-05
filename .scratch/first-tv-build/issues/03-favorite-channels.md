# 03 — Keep favorite channels in Home and the Guide

**What to build:** Favorite or unfavorite a channel with the remote and find the same saved choices in Home and the Guide after restarting.

**Blocked by:** 02 — Connect a provider and watch its channels without guide data

**Status:** ready-for-agent

**Type:** task

- [ ] Favorite and unfavorite actions are reachable from channel browsing with the remote.
- [ ] Home and the Guide expose the same provider-scoped favorites, and selecting an available favorite starts playback directly.
- [ ] Favorites survive app/process restart and catalog refresh, including a changed provider listing order.
- [ ] A favorite whose source channel disappears is retained as unavailable rather than silently reassigned using a row index or matching name.
- [ ] An empty Favorites section offers a useful route to browse channels instead of requiring setup or fabricating content.
- [ ] Behavioral tests cover favorite changes, direct playback, persistence, and refresh/disappearance cases.
