# First native TV build

Status: needs-info

Proposed implementation milestone, awaiting confirmation of shared understanding. The full [product discovery spec](../product-discovery/spec.md) remains the public-release contract; this milestone stages the work so the core experience can be tested on the user's Google TV first.

## Outcome

A viewer can enter an Xtream Codes connection on the TV, find and favorite a channel, watch it, browse other channels without interrupting playback, return to Home or Guide with a mini player, and reopen the app with personal choices intact. Missing guide data never prevents channel discovery or playback.

## Included in the first build

- An installable native Android TV app using Kotlin, Compose for TV, and one Media3 playback integration, with reproducible build instructions.
- Direct TV entry and saved provider connections, with separate lineups and provider-defined groups.
- Home with favorite and recent channels; a channel-list Guide with a compact personal section, simple channel-name search, and remote-usable hide/reorder controls.
- Full-screen playback, a compact channel browser, and the mini player on Home/Guide. Available stream capabilities determine transport controls; browsing alone never tunes another channel.
- Optional program information and readable fallbacks for missing listings or logos. No fabricated program titles, progress, or artwork.
- Durable local favorites, recents, visibility, and order, with one default profile. Room/SQLite and small-preference DataStore are the proposed persistence implementation.
- Bounded recovery for transient startup failures, actionable failure states, and responsive Back/channel selection while requests are pending.

## Proposed interaction defaults to validate

These make the first build concrete; they are part of the proposal, not additional previously accepted interview answers.

- Home places Favorites before Recents initially. Before either exists, it offers a direct route to browse the selected provider's channels without requiring a favorites setup exercise.
- Back closes a visible overlay first. Leaving full-screen playback returns to the originating browsing view and relevant focused item, with the active video in the mini player. Selecting the mini player returns to full screen.
- Browsing another provider changes the visible lineup; it does not retune the playing channel until a new channel is explicitly selected. The mini player identifies the source of the active channel.
- Restoring focus uses channel identity and saved context, with a visible fallback if that item has disappeared. Refreshes preserve personal choices and avoid unexpectedly moving focus.
- Leaving the app for the TV's system home pauses video; returning offers usable playback controls rather than allowing hidden audio to continue.

## Later work still required for public release

- QR phone setup, the encrypted relay, its hosting, and protocol validation.
- Seven-day trial and permanent Google Play unlock, including price, eligibility, expiry/offline behavior, verification, and restoration.
- The schedule-grid presentation and fuller program-detail behavior when useful guide data exists.
- Final visual refinement, accessibility and device qualification, store assets/review, and production packaging.
- Fire OS expansion after Google/Android TV, with its own device validation and distribution work.

The first internal test build would remain unlocked and use direct TV setup. This is a development stage, not a change to the agreed public-release requirements. Movies/series, recordings, provider catch-up, cloud profile sync, and a dedicated live buffer stay outside the first public release as already agreed.

## Evidence expected

1. Build an installable APK and run meaningful tests for provider-data handling, absent EPG, personal-state persistence, provider separation, and stale playback callbacks.
2. Exercise D-pad navigation, overlay/mini/full-screen transitions, explicit channel switching, and returning to the prior browsing context.
3. Verify favorites/recents and organization after process/app restart and catalog refresh.
4. Test required real streams on the user's TV, including failed starts and supported audio/subtitle/control behavior. Device-dependent results remain unverified until those tests actually occur.
5. Deliver the source, APK, build/test instructions, and an honest record of passed checks and remaining device checks.

## Preparation and boundaries

The repo currently contains discovery documents, not an Android app. The environment inventory found Java installations and Gradle files, but no Android SDK/Studio/command-line tools in the checked standard locations. Building requires preparing a compatible Android toolchain; the exact TV model/OS and installation/debugging setup are needed before physical-device validation. See [environment inventory](../product-discovery/development-environment.md).

No app code, infrastructure deployment, real billing configuration, or store submission is authorized by this proposal alone. Confirmation of this milestone starts implementation; public release still requires the later work and demonstrated acceptance.

## Comments

### 2026-10-04 — Proposed after discovery

This milestone concentrates the agreed product direction into a testable native viewing loop. It is proposed before spending implementation effort on billing or the hosted phone-setup service, because real navigation and playback evidence should inform the remaining release work.
