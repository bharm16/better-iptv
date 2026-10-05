# First native TV build

Status: ready-for-agent

The user approved the 14-ticket milestone on 2026-10-04. The [interaction contract](interaction-contract.md) records the subsequent architecture-review refinements and is the detailed behavior baseline for this build. Implementation and all acceptance checks remain unperformed. The full [product discovery spec](../product-discovery/spec.md) remains the public-release direction; this milestone stages the viewing loop for testing on the user's Google TV first.

## Outcome

A viewer can enter an Xtream Codes connection on the TV, find and favorite a channel, watch it, browse other channels without interrupting playback, return to Home or Guide with a mini player, and reopen the app with personal choices intact. Missing guide data never prevents channel discovery or playback.

## Included in the first build

- An installable native Android TV app using Kotlin, Compose for TV, and one Media3 playback integration, with reproducible build instructions.
- Direct TV entry and saved provider connections, with separate lineups and provider-defined groups.
- Home with favorite and recent channels; a channel-list Guide with a compact personal section, simple channel-name search, and remote-usable hide/reorder controls.
- Full-screen playback, a compact channel browser, and the mini player on Home/Guide. Available stream capabilities determine transport controls; browsing alone never tunes another channel.
- Optional program information and readable fallbacks for missing listings or logos. No fabricated program titles, progress, or artwork.
- Durable local favorites, recents, visibility, and order, with one default profile. Room/SQLite and small-preference DataStore are the proposed persistence implementation.
- Finite, documented recovery for initial starts, channel replacement and interruptions after playback starts, with distinct Connecting, Buffering, Reconnecting, actionable failure and Stream ended states on the current player surface.
- Explicit Back precedence, remote-reachable Stop, stable return focus, provider-scoped navigation and suspension/warm-return behavior.

## Interaction behavior

The [event, Back, lifecycle and task-flow tables](interaction-contract.md) resolve the detailed behavior. Physical remote mapping and exact numeric budgets still require implementation-time choice and device testing.

- Home places Favorites before Recents initially. Before either exists, it offers a direct route to browse the selected provider's channels without requiring a favorites setup exercise.
- Back dismisses the top interaction layer first. A bare full-screen initial/replacement attempt can then be cancelled to browsing without active video. An established session, including ongoing recovery, returns to browsing in the mini player. Stop ends the session separately.
- Explicitly selecting B replaces A; failure or cancellation does not silently restart A. Selecting a channel/Favorite/Recent watches live, while mini-player expansion changes presentation without retuning, resuming or seeking.
- Browsing another provider changes the visible lineup; it does not retune the playing channel until a new channel is explicitly selected. The mini player identifies the source of the active channel.
- Capture browsing context on each full-screen channel selection or mini-player expansion. Back restores that latest origin by identity, then a surviving item or enabled selector/Browse/Manage control. Refreshes preserve personal choices and do not steal focus.
- Global Guide restores the browsed provider; All channels · Provider A in A's compact browser deliberately opens A's Guide without tuning.
- Backgrounding suspends playback and recovery, allowing player resources to be released. Warm return restores context with an explicit playback action, conditional on position validity. Fresh launch/process recreation opens Home without autoplay.
- Favorites, hide/restore, reorder, Details and track menus have visible remote entries, completion/cancellation behavior and focus rules in the interaction contract. Reorder uses a draft and queues catalog reconciliation; Recents stays chronological.

## Unresolved details required within the first build

- Finite startup/buffering/reconnect attempt and elapsed-time values, plus failure classification, selected and tested before acceptance.
- Missing/invalid/stale program-information policy and copy, and the basic Details action with top-layer dismissal; these are not deferred to a later release.
- Exact remote mapping and control placement; all essential actions remain visible and reachable without long-press-only gestures.

## Later work still required for public release

- QR phone setup, the encrypted relay, its hosting, and protocol validation.
- Seven-day trial and permanent Google Play unlock, including price, eligibility, expiry/offline behavior, verification, and restoration.
- The schedule-grid presentation and richer program discovery beyond the basic Details action already required in this build.
- Final visual refinement, accessibility and device qualification, store assets/review, and production packaging.
- Fire OS expansion after Google/Android TV, with its own device validation and distribution work.

The first internal test build would remain unlocked and use direct TV setup. This is a development stage, not a change to the agreed public-release requirements. Movies/series, recordings, provider catch-up, cloud profile sync, and a dedicated live buffer stay outside the first public release as already agreed.

## Evidence expected

1. Build an installable APK and run meaningful tests for provider-data handling, absent EPG, personal-state persistence, provider separation, and stale playback callbacks.
2. Exercise D-pad navigation, overlay/mini/full-screen transitions, Back/Stop, explicit replacement and cancellation, provider-scoped navigation, and returning to the latest browsing context.
3. Verify favorites/recents and organization after process/app restart and catalog refresh.
4. Test required real streams on the user's TV, including failed starts, mid-stream interruption, ended streams, mini-player recovery, suspension/return, and supported audio/subtitle/control behavior. Device-dependent results remain unverified until those tests actually occur.
5. Deliver the source, APK, build/test instructions, and an honest record of passed checks and remaining device checks.

## Preparation and boundaries

The repo currently contains discovery documents, not an Android app. The environment inventory found Java installations and Gradle files, but no Android SDK/Studio/command-line tools in the checked standard locations. Building requires preparing a compatible Android toolchain; the exact TV model/OS and installation/debugging setup are needed before physical-device validation. See [environment inventory](../product-discovery/development-environment.md).

Planning approval and this documentation revision do not claim implementation or device acceptance. The current work remains behavior/design preparation; app implementation, infrastructure deployment, billing configuration and store submission are separate work. Public release still requires the later scope and demonstrated acceptance.

## Comments

### 2026-10-04 — Proposed after discovery

This milestone concentrates the agreed product direction into a testable native viewing loop. It is proposed before spending implementation effort on billing or the hosted phone-setup service, because real navigation and playback evidence should inform the remaining release work.

### 2026-10-05 — Approval status and architecture-review refinement

The user approved publication of the 14 tickets. The subsequent architecture review corrected group selection, clarified replacement/cancellation, provider return context and suspension, and added ongoing recovery and Stop to the first-build behavior. Basic Details/stale-data handling and finite recovery budgets remain first-build requirements. The current status reflects planning readiness, not completed acceptance.
