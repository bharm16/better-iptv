# 08 — Browse channels over full-screen playback

**What to build:** Open a compact channel browser while a channel remains full-screen, inspect favorites and recents, and switch only after an explicit selection.

**Blocked by:** 03 — Keep favorite channels in Home and the Guide; 04 — Return to recently watched channels

**Status:** ready-for-agent

**Type:** task

- [ ] The channel browser is reachable with a standard TV remote and exposes favorites and recents for the playing provider, with visible provider context.
- [ ] Moving focus or opening/closing the browser does not retune, recreate, or interrupt the active playback owner.
- [ ] Selecting an available channel explicitly switches the stream; Back closes the overlay and leaves the current channel playing.
- [ ] Focus is visible and predictable, including empty personal lists and missing program information.
- [ ] All channels · Provider A in A's compact browser deliberately opens A's Guide without tuning; the separate global Guide destination restores the last browsed provider.
- [ ] Interaction tests verify open, navigation, explicit switching, and Back, including that browsing alone makes no new playback request.
