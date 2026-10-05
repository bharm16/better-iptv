# 06 — Recover failed channel starts without trapping navigation

**What to build:** When a channel fails to start, recover briefly from transient failures or offer clear Retry and Choose another channel actions while the viewer remains in control.

**Blocked by:** 02 — Connect a provider and watch its channels without guide data

**Status:** ready-for-agent

**Type:** task

- [ ] Transient startup failures use a finite, documented retry/time budget; definitive failures do not enter an indefinite retry loop.
- [ ] After the budget is exhausted, the viewer can retry the selected channel or return to channel browsing.
- [ ] Back and selecting another channel cancel obsolete recovery work promptly.
- [ ] Late success/error callbacks from an old request cannot replace the newly selected channel's state or retune it.
- [ ] Failure messages and diagnostics identify useful failure categories without exposing credentials or private playback URLs.
- [ ] Controlled-failure tests prove budget exhaustion, manual retry, cancellation, and stale-callback behavior.
