# 06 — Recover channel starts and interrupted playback

**What to build:** Recover within finite limits when a selected channel fails to start or established playback is interrupted, with clear outcomes and responsive navigation on the current player surface.

**Blocked by:** 02 — Connect a provider and watch its channels without guide data

**Status:** ready-for-agent

**Type:** task

- [ ] Startup, buffering and reconnection each have a finite, documented attempt/time budget and failure classification; definitive failures bypass automatic retry. Exact values are selected and qualified within this build.
- [ ] Selecting B replaces playing/paused A immediately and shows Connecting B. If B fails or is cancelled, A is not silently restarted.
- [ ] Cancelling a bare full-screen initial/channel-switch/manual-retry attempt returns to its captured browser without active video. Back dismisses a higher interaction layer first; selecting another channel or Stop cancels obsolete work promptly.
- [ ] After startup failure, Retry starts a new bounded attempt for that named channel; Choose another or Back from its bare full-screen failure clears the failed player and restores the originating browser and focus.
- [ ] After playback starts, temporary buffering, reconnecting, terminal playback failure and a stream ending remain distinct states; intentional pause/suspension is not inferred to be an error from a generic not-playing signal.
- [ ] Ongoing recovery reaches Playing or an actionable failure within its budget in the existing full-screen player and preserves current view/focus; ticket 09 adds mini-player integration and verifies that it cannot take over the Guide or steal browsing focus.
- [ ] An ended stream offers Watch live again, Choose another and Stop without an endless restart loop. Terminal/exhausted failure offers Retry, Choose another and Stop.
- [ ] Late success/error callbacks from an old request cannot replace the newly selected channel's state or retune it.
- [ ] Failure messages and diagnostics identify useful failure categories without exposing credentials or private playback URLs.
- [ ] Controlled-failure tests cover initial start, A-to-B replacement, Back precedence, cancellation, stalls after successful playback, terminal errors, end-of-stream, budget exhaustion, manual retry and stale callbacks.

## Comments

### 2026-10-05 — Architecture review refinement

Ongoing-playback recovery is an explicit addition to the original startup-only slice. The [interaction contract](../interaction-contract.md) defines the event and return-focus behavior; implementation and acceptance remain unperformed.
