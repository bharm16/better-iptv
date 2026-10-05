# IPTV app product discovery

Status: needs-info

Working record of the product interview. This is not an approved implementation spec.

The [approved first-build scope](../first-tv-build/spec.md) and [interaction contract](../first-tv-build/interaction-contract.md) now define the initial implementation behavior, including subsequent architecture-review refinements. Open questions below reflect interview history; resolved first-build behavior is recorded in those current documents.

## Confirmed direction

- Build a better IPTV / Xtream Codes app, starting with Android TV.
- Support Xtream Codes connections in the first public release: the viewer supplies a provider server address, username, and password. M3U playlist and separate XMLTV imports are deferred.
- Support both provider setup paths: scan a QR code on the TV and enter connection details on a phone, or enter those details directly on the TV with the remote. Phone setup is optional.
- Use an accountless hosted relay for temporary encrypted phone-to-TV setup messages. The intended design encrypts provider details for the selected TV before relay upload and removes relay data after delivery or expiry. Direct TV entry and normal viewing do not depend on the setup relay; the concrete protocol and hosting remain to be validated. See [ADR 0004](../../docs/adr/0004-temporary-encrypted-setup-relay.md).
- Allow multiple saved provider connections, with one provider's lineup shown at a time. Home and the guide reflect the selected provider; the first release does not combine providers into one lineup.
- Preserve provider-defined channel groups while allowing viewers to hide and reorder groups and channels. Organization is optional; viewers can start watching without first curating the lineup. These are app viewing preferences, not changes to the provider's catalog.
- Aim for public release, with the user testing early builds first. The product is not scoped as a personal-only or household-only app.
- Use Google Play for the first public Google/Android TV release, with direct installation of early builds for personal testing. Public APK distribution is not part of the selected launch route. Store readiness and approval remain to be demonstrated.
- Offer a free download with a full seven-day trial starting at the first successful channel playback, followed by an explicit one-time Google Play purchase to unlock continued app access. Installation and failed setup do not start the trial. There are no app-inserted ads. Price, eligibility/reset rules, and expiry/offline behavior remain unresolved. The purchase concerns the player app, not access supplied by a provider. See [ADR 0005](../../docs/adr/0005-trial-before-permanent-unlock.md).
- Use the user's TV with built-in Google TV for the first hands-on tests, as reported by the user. The exact model, OS version, and test-build installation method can be confirmed before device-specific validation.
- After Google/Android TV, target Fire TV devices running Android-based Fire OS. Apple TV and Vega OS are later possibilities, not the next selected port. Other TVs and streaming boxes remain higher priority than phones, tablets, desktop, or web; qualified device/OS versions are unresolved.
- Use Kotlin, Compose for TV, and Media3/ExoPlayer as the initial implementation stack, following the user's conditional acceptance and the completed comparison. Actual dependency pins and device/provider qualification remain open. See [ADR 0003](../../docs/adr/0003-native-android-tv-foundation.md).
- Improve navigation and usability, playback reliability, content organization, and visual design.
- Start the design discussion with navigation and usability. The other three areas remain in scope; their release requirements are not yet defined.
- Scope the first public release to live TV: personal Home, program guide, channel organization, and playback. Movies and series are deferred until after that release.
- Defer both manual and scheduled recording from the first public release. A saved-recordings library and DVR workflows are outside that release's scope.
- Defer provider catch-up from the first public release: no browsing or playback of provider-archived earlier broadcasts. Supported pause/rewind within the active live stream remains in scope.
- Offer pause and rewind according to the active stream/player's actual capabilities and available window. A dedicated app-managed temporary TV buffer is deferred from the first release; pause/resume and rewind limits may therefore vary by stream.
- When a channel fails to start because of a transient failure, attempt brief automatic recovery within a limit, then offer clear Retry and Choose another channel actions. Navigation and channel switching remain responsive during recovery; retry budgets and failure classification still need definition.
- Give returning viewers a personal starting experience with favorites and recent channels. The user rejected a bare guide that makes them start from zero each time.
- Home leads with favorite and recent channels, not a program-led "what's on now" feed. Program information is optional enrichment; the exact order of favorites and recents is still open.
- Channel discovery and playback must remain usable when guide data is missing or unreliable. The guide, Home, and channel browser cannot require current program titles, timings, or artwork to expose a playable channel.
- When a provider has little usable schedule information, the Guide defaults to a channel list with groups and favorites. A schedule grid remains available when useful listings exist; program information supplements channel browsing rather than determining whether channels appear.
- On a fresh launch, open Home without starting video or audio automatically. Playback begins when the viewer selects a channel; the last watched channel remains easy to reach through recent channels.
- Selecting a channel, or a currently airing program when available, starts full-screen playback immediately. Available program details remain accessible through a separate action rather than a required intermediate screen.
- Provide both a dedicated personal Home view and a program guide with a compact favorites/recent-channels section. Favorites and recent viewing represent the same personal data in both views.
- During playback, channel browsing opens a compact overlay first, showing recent channels and favorites, with program information when available, while the existing video stays full-screen. The full guide remains accessible. Browsing alone keeps the current channel playing; selecting another channel changes it.
- Returning to Home or opening the full Guide inside the app keeps the active channel playing in a small video window. This concerns existing playback; fresh launches still open Home without autoplay.
- Start with one default viewer profile owning favorites, history, and viewing preferences. Optional additional profiles are an agreed future direction, but profile management is deferred and is not a requirement for the first build.
- Save favorites, recent channels, and channel organization on each device, retaining them across app and TV restarts. The first release does not require an app account; cross-device synchronization is deferred.

## Provider-data constraint

The user reports that the providers they have used often lack reliable, up-to-date program listings. Treat sparse or unavailable guide data as a normal condition in this product's design. This is a user-reported constraint, not a verified claim about every provider; actual compatibility and data quality still need testing.

See [Channel access is independent of guide data](../../docs/adr/0001-channel-access-independent-of-guide-data.md).

## Open decisions

- The precise layout and controls connecting Home, the personalized guide, and playback.
- The ordering and presentation of favorites and recents on Home.
- How missing or stale information is communicated, and how viewers move between channel-list and schedule-grid presentations without losing their place.
- How viewers access program details, and what selecting an upcoming program does.
- Where organization controls live, how hidden items behave across views, and how personal ordering survives provider updates.
- What browsing position and focus are restored between views or visits, and how that restoration handles schedule or channel changes.
- Remote-control navigation.
- How the player communicates unavailable controls or an expired paused position.
- Concrete startup/recovery time budgets and error classification for the agreed bounded recovery behavior.
- Target audience within the public IPTV market, trial eligibility/reset/expiry/offline rules, purchase restoration and verification, price, and later Fire OS distribution.
- How personal testing leads to public-release acceptance.
- Concrete problems in existing apps and the behavior that should replace them.
- Provider compatibility and supported capabilities.
- The hosted setup relay's operating model and concrete protocol: correct-TV binding, encryption, expiry, retries, and hosted-page trust.
- Provider-switching and return-focus behavior while the active channel remains in the mini player.
- Later timing for additional viewer profiles; cross-device synchronization is outside the first release.
- The model, OS version, and installation method for the user's built-in Google TV, plus the device/OS support matrix for Android TV and Fire OS.
- Detailed module, persistence, and setup-handoff boundaries, and the pinned dependency/OS compatibility matrix.
- First-version boundaries and acceptance criteria.

## Comments

### 2026-10-04 — Interview format

The user requested one question at a time, with multiple-choice answers and a recommended answer.

### 2026-10-04 — Quality priorities

The user confirmed that all four quality areas matter and chose navigation and usability as the starting focus: "yes we need to hit all of these but lets start with A".

### 2026-10-04 — First viewing workflow

The user accepted the recommendation to design live TV first, including the program guide and channel switching.

### 2026-10-04 — Personal starting experience and UX research

The user chose a home screen with favorites and recent channels, explaining that current apps open a guide and make the viewer start from zero every time. They suggested that home might be within the guide and requested research into established TV UX from cable providers, Sling, Fubo, and similar services before choosing a layout.

The earlier guide-first recommendation was not accepted. Research findings are recorded in [TV UX research](./research-tv-ux.md); recommendations there remain proposals until discussed.

### 2026-10-04 — Primary UX comparisons

The user specifically emphasized Fubo, Sling, and YouTube TV as analogous products. Research should center those TV experiences, with cable-provider and platform guidance as supporting references.

### 2026-10-04 — Research outcome and proposed next decision

The research found recurring personal shortcuts across Home, guide, and playback, rather than one universal layout. The revised recommendation is to explore a compact favorites/recent-channels section connected directly to the full guide, compared with adjacent Home and Guide views sharing the same personal state. Neither layout has been selected. Preserving personal data and browsing context is a proposed behavior contract to resolve alongside the layout.

### 2026-10-04 — Home and personalized guide

The user chose both options. The working direction is a dedicated personal Home view alongside a guide that also includes compact favorites and recents. The two views share personal channel data; the layout, controls, state-restoration rules, and ownership of that data remain to be resolved.

### 2026-10-04 — Public release with personal testing first

The user clarified: "the goal is public release but I will test it first". Public release is the intended outcome; personal testing is the initial validation stage. Audience details, distribution, pricing, and public-release acceptance remain open.

### 2026-10-04 — Initial connection support

The user accepted Xtream Codes as the only connection method for the first public release. The setup flow uses a provider server address, username, and password. M3U channel-list imports and separate XMLTV guide-feed imports are deferred; no implementation technology or provider-compatibility guarantee has been selected.

### 2026-10-04 — Live-TV scope for public launch

The user accepted a live-TV-only first public release, with movies and series deferred. This settles release scope beyond the earlier decision to design live TV first. Home, guide, channel organization, playback reliability, and visual quality remain part of that release; specific acceptance criteria and live-TV extras remain open.

### 2026-10-04 — Multiple saved providers

The user accepted saving multiple provider connections and switching between their separate channel lineups and guides. The selected provider supplies the content shown in Home and the guide. Combining multiple providers into one lineup is outside the first-release scope; provider-switching controls, playback effects, and restoration behavior remain open.

### 2026-10-04 — One default profile first

The user accepted the direction of optional viewer profiles but explicitly deprioritized it: "this isnt the focus we'll start with one". Initial builds use one default profile. Additional-profile creation and switching are deferred; the user has not made them a first-public-release requirement. Keep the current design work focused on the live-TV viewing experience.

### 2026-10-04 — Channel browsing during playback

The user accepted a compact channel browser as the first browsing view during playback. It surfaces recent channels, favorites, and what is on while the current channel continues full-screen; the full guide remains reachable. The exact remote mapping and full-guide playback layout remain open.

### 2026-10-04 — Home without autoplay

The user accepted opening Home on a fresh app launch without starting video or audio. Favorites, recent channels, and current program information are available for browsing; playback starts after an explicit channel selection. This decision covers fresh launch and does not determine how an already playing channel is presented when navigating back to Home or the full guide.

### 2026-10-04 — Direct playback for current programs

The user accepted starting full-screen playback immediately when selecting a program airing now. Program details remain accessible through a separate action. The specific details control, behavior for upcoming programs, and behavior for unavailable guide information remain open.

### 2026-10-04 — Viewer-controlled lineup organization

The user accepted keeping provider-defined groups with controls to hide and reorder groups and channels. This customization is optional so that initial viewing does not depend on an organization task. Automatically replacing provider groups with app-generated categories is not the chosen approach.

### 2026-10-04 — Channels lead; guide data is optional

The user chose favorites and recents instead of the proposed current-program-led Home. They explained that their providers often have poor or outdated guide information. Home should therefore be useful through channel identity and personal history, with program data added when available. This corrects the earlier assumption that current program information would be a reliable foundation for the main experience.

### 2026-10-04 — Guide with sparse listings

The user accepted a channel-list default when a provider has little usable schedule data, with a schedule grid available when listings are useful. Guide now names the main channel-browsing destination; the schedule grid is one possible presentation within it. The rules for choosing or changing presentation, and preserving position across data refreshes, remain open.

### 2026-10-04 — Two provider setup paths

The user explicitly chose both options: QR-based setup from a phone and direct entry on the TV. Both are supported setup paths; viewers are not required to use a phone. The handoff mechanism, any backend involvement, and credential handling remain design work rather than selected implementation details.

### 2026-10-04 — Personalization saved on each device

The user accepted storing favorites, recents, and channel organization on each device for the first release, with persistence across app and TV restarts and no required app account. Cross-device synchronization is deferred. This does not determine the phone-setup handoff mechanism or authorize storing provider credentials in a cloud service. See [Device owns personalization in the first release](../../docs/adr/0002-device-owns-personalization.md).

### 2026-10-04 — Recording deferred

The user accepted deferring recording from the first public release. This includes manual recording, scheduled recording, and saved-recording management. It does not settle whether playback should support pausing or seeking within a stream's available live window, or whether the app should maintain its own temporary time-shift buffer.

### 2026-10-04 — Pause and rewind research

[Live playback research](./research-live-playback.md) distinguishes controls supported by the current stream/player, an app-managed temporary viewing buffer, saved recordings, and provider catch-up. Guide-data availability does not establish rewind availability. No actual provider stream or TV hardware has been tested; the first-release commitment to temporary buffering remains a user decision.

### 2026-10-04 — Available playback controls first

The user accepted using each channel's available playback capabilities for pause and rewind in the first release, with a dedicated temporary TV buffer deferred. The discussed tradeoff is that rewind availability and pause/resume limits vary by stream, including the possibility that a paused position outlasts the available live window. Player technology, actual provider compatibility, and the recovery interaction remain unresolved.

### 2026-10-04 — TV platforms before other form factors

The user accepted prioritizing other TVs and streaming boxes after Android TV. Apple TV and Fire TV were examples in the question, not a selected implementation order or a commitment to every model. Phone, tablet, desktop, and browser experiences are lower priority; the next concrete TV target and the code-sharing strategy remain open.

### 2026-10-04 — Existing TV setup for initial testing

The user chose their own TV for the first round of testing. The exact model and app-running device have not been supplied, so Android TV/Google TV compatibility and the installation path are not yet verified.

### 2026-10-04 — Built-in Google TV test host

The user clarified that the TV runs Google TV natively. Use that built-in app environment as the first test target. The brand/model and precise OS version remain unknown, but they are not required to continue product discovery; confirm them before device-specific compatibility or installation claims.

### 2026-10-04 — Platform boundaries researched

[TV platform research](./research-tv-platforms.md) distinguishes Android-based Fire OS from Vega OS and documents the boundaries of native, Kotlin Multiplatform, and React Native TV approaches. These are implementation candidates and platform facts, not an accepted stack or next-platform decision. No app or device compatibility was tested.

### 2026-10-04 — Fire OS as the next TV target

The user accepted Fire TV devices running Android-based Fire OS as the next platform after Google/Android TV. This does not include Fire TV models running Vega OS. The supported Fire OS versions/models, distribution path, and validation requirements are still to be established; the user has not yet chosen the implementation stack.

### 2026-10-04 — Native stack subject to research

The user accepted the native Android recommendation provisionally and requested research first to ensure it is the best stack. Compare native Kotlin/Compose for TV/Media3 with credible cross-platform TV alternatives and playback engines against the agreed product and platform scope. Documentation support must be distinguished from actual device, provider, and performance validation.

### 2026-10-04 — Stack research assessed

[The completed stack comparison](./research-stack.md) supports Kotlin, Compose for TV, and Media3 as the best-supported fit for the selected Google/Android TV then Fire OS roadmap. React Native TV is the strongest alternative; Flutter has less complete TV-specific support evidence. Research refines the approach toward a dedicated video surface, one initial playback engine, and durable personalization separate from transient UI state. Room/SQLite and DataStore are proposed supporting persistence components. The working stack is recorded in ADR 0003; no app was implemented or benchmarked, and actual stream/device qualification remains required.

### 2026-10-04 — Bounded recovery when a channel fails to start

The user accepted a brief automatic recovery attempt for transient startup failures, followed by clear Retry and Choose another channel actions. Navigation stays responsive during recovery. This is not an indefinite retry policy; specific limits, error classification, and handling of failures during an already playing stream remain to be defined.

### 2026-10-04 — Google Play public distribution

The user accepted Google Play as the first public distribution route, with direct installs used for early testing on their TV. No app submission or publication has occurred. The [Android TV distribution guide](https://developer.android.com/training/tv/publishing/distribute) is the source for the eventual TV review and packaging requirements; these are release gates, not completed acceptance evidence.

### 2026-10-04 — Phone setup feasibility researched

[Phone-to-TV setup research](./research-phone-setup.md) compares direct LAN setup, a hosted HTTPS page with a temporary encrypted relay, and platform phone keyboards. Browser trust/network constraints make a generic LAN-only QR form a nontrivial compatibility task. The proposed public-release approach is an accountless, short-lived encrypted setup relay plus direct TV entry, but operating a hosted service is not yet accepted. This would be a separate transient setup flow, not cloud profile synchronization or a persistent plaintext credential store; the protocol and hosted-page trust still require validation.

### 2026-10-04 — Temporary hosted setup relay

The user accepted operating a hosted encrypted relay for QR setup. This resolves the service-ownership choice while preserving direct TV entry, device-local favorites/history, and no required app account. Hosting, the message protocol, keys, expiry, abuse controls, and deployment are not yet selected or implemented. The intended relay handles temporary ciphertext, not a persistent plaintext provider-credential vault.

### 2026-10-04 — One-time purchase without app advertising

The user accepted a one-time purchase model with no app-inserted ads. This does not specify a price, trial, upfront paid download, or permanent in-app unlock yet. [Monetization research](./research-monetization.md) records the different Google Play models and their constraints. No billing product, pricing, or payment flow has been created.

### 2026-10-04 — Full trial before one-time unlock

The user accepted a free download with a full trial so viewers can test their provider and TV before paying, then an explicit one-time in-app unlock through Google Play. The trial is app-managed rather than a subscription free-trial phase. Duration, start trigger, eligibility/reset behavior, expiry/offline behavior, restoration, verification, and price are not yet selected. The user was informed that a free-download listing cannot later become a paid-download listing, while an in-app unlock remains possible.

### 2026-10-04 — Seven days from successful playback

The user accepted a full seven-day trial beginning with the first successful playback, rather than installation or failed setup attempts. This is elapsed trial time, not an accumulated playback-time allowance. The exact success signal and timekeeping, eligibility/reset behavior, and how expiry affects an active viewing session remain implementation/product details to resolve before release.

### 2026-10-04 — Provider catch-up excluded from launch

Asked whether launch should include provider catch-up, the user answered "no". Provider-archived replay browsing and playback are deferred. This does not remove the already accepted pause/rewind controls available within a currently playing live stream.

### 2026-10-04 — Mini player in Home and Guide

The user accepted keeping the active channel playing in a small video window when returning to Home or opening the full Guide within the app. The compact channel browser remains the first browsing view over full-screen playback; Home/Guide use the mini player. Fresh-launch behavior remains explicitly without autoplay.

### 2026-10-04 — First build proposed for confirmation

The [first native TV build](../first-tv-build/spec.md) proposes validating direct TV setup, personal channel browsing, playback, overlays/mini player, and persistence before the later QR-service, billing, schedule-grid, and public-release work. Its additional interaction defaults are explicitly proposed for review. App implementation has not started; the milestone awaits confirmation of shared understanding.
