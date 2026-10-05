# Product discovery map

## Notes

This is an active interview, not implementation authorization. Ask one question at a time with multiple-choice answers and a recommendation. The [working spec](./spec.md) records accepted decisions and the conversation; [TV UX research](./research-tv-ux.md) supplies evidence, not automatic product commitments.

## Decisions-so-far

- **Release goal:** a public Android TV app, personally tested by the user first.
  - Initial hands-on testing uses the user's TV with built-in Google TV. Exact model and OS version remain to be confirmed before device-specific validation.
  - First release covers live TV.
  - Google Play is the public launch route; early personal testing uses direct installs. Store readiness/approval remain open.
  - Free download and a full seven-day trial beginning at first successful playback precede an explicit one-time Google Play unlock, without app-inserted ads. Price and detailed eligibility/expiry rules remain open; see [ADR 0005](../../docs/adr/0005-trial-before-permanent-unlock.md).
  - Movies, series, recording, provider catch-up, and cross-device synchronization are deferred.
  - Fire OS-based Fire TV devices come next after Google/Android TV; Vega OS and Apple TV are later possibilities. Phones, tablets, desktop, and web are lower priority. Qualified devices remain unresolved.
  - Kotlin, Compose for TV, and Media3 are selected following the user's conditional acceptance and [stack research](./research-stack.md); see [ADR 0003](../../docs/adr/0003-native-android-tv-foundation.md).
- **Provider access:** Xtream Codes connections.
  - Support phone setup via a TV QR code and direct TV entry.
  - Use a temporary encrypted setup relay without viewer accounts; hosting/protocol are still unvalidated. See [ADR 0004](../../docs/adr/0004-temporary-encrypted-setup-relay.md).
  - Save multiple connections; browse one provider's lineup at a time.
  - Keep provider groups; allow optional hiding and reordering.
- **Personal viewing:** Home and Guide both expose favorites and recents.
  - One default profile first; additional-profile management is deferred.
  - Save personal channel data on each device across app and TV restarts.
  - Home opens without autoplay and leads with channels, not program recommendations.
- **Guide data:** optional enrichment, with unreliable listings treated as a normal design condition.
  - Use a channel list when schedule data is sparse; offer a grid when useful listings exist.
  - Finding and playing a channel must not require schedule data.
  - See [ADR 0001](../../docs/adr/0001-channel-access-independent-of-guide-data.md).
- **Watching:** selecting a channel/current program starts full-screen playback.
  - Program details use a separate action.
  - Open a compact channel browser over active playback first; retain access to the full Guide.
  - Browsing alone keeps the current channel playing.
  - Home and the full Guide keep the active channel playing in a small video window.
  - Pause and rewind use the active playback's supported capabilities and available window; a dedicated temporary TV buffer is deferred.
  - Transient channel-start failures get bounded automatic recovery, then Retry/Choose another channel actions; navigation remains responsive.

## Fog

The following branches remain open. Recompute their order as the user answers; do not turn unaccepted research recommendations into requirements.

1. **Playback scope and behavior**
   - Communicating unavailable playback controls or an expired paused position.
   - [Live playback research](./research-live-playback.md) establishes the capability distinctions; stream and device validation are still outstanding.
   - Provider catch-up is excluded from launch; active-stream pause/rewind stays within supported capabilities.
   - Exact startup/recovery budgets and failure classification; recovery behavior when an already playing stream fails.
   - These decisions precede detailed player controls and remote mapping.
2. **Continuity between views**
   - Return focus and position and provider switching during playback; active video presentation in Home/Guide is settled as a mini player.
   - Handling refreshed/removed channels, hidden items, and changing schedule data.
   - Favorites-versus-recents ordering and the first-use state before either exists.
3. **Platform and delivery boundaries**
   - Exact model/OS version of the user's built-in Google TV and the Android TV/Fire OS device support matrix.
   - [TV platform research](./research-tv-platforms.md) documents runtime boundaries. Google/Android TV then Fire OS is the selected order, using Kotlin/Compose for TV/Media3; dependency pins and qualification remain open.
   - Price, trial eligibility/reset/expiry/offline rules, purchase verification/restoration, Google Play readiness/review, later Fire OS distribution, and how personal testing proves public-release readiness.
   - [Monetization research](./research-monetization.md) supports the distinction between app-managed trial and permanent Google Play unlock; that model is selected, with detailed rules still open.
   - The selected stack still needs concrete module/persistence boundaries and a validated dependency/device matrix.
4. **Agent-owned investigation**
   - Verify playback capabilities and provider-data behavior from appropriate primary evidence.
   - [Phone setup research](./research-phone-setup.md) documents LAN/browser constraints. The user accepted an accountless temporary encrypted relay; its concrete protocol and hosting remain unvalidated.
   - Gather implementation and platform facts; ask the user for preferences and scope rather than facts the agent can look up.

Before implementation, summarize the resulting product and behavior contract for the user's confirmation of shared understanding.

The user confirmed the [first native TV build scope](../first-tv-build/spec.md) and approved the [14-ticket breakdown](../first-tv-build/ticket-breakdown.md) for local publication and Git push. The [first-build ticket map](../first-tv-build/map.md) links the individual files and blocking edges. The current pass is documentation/ticket work only; no app implementation or acceptance checks have occurred. Remaining public-release questions stay visible above and in the main spec.
