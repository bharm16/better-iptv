# First-build interaction contract

Planning status: the 14-ticket first-build scope was approved on 2026-10-04. This revision was prepared on 2026-10-05 from the architecture review received on 2026-10-04. Implementation and acceptance testing remain unperformed.

This contract supplements the [first-build spec](spec.md) and the [UX architecture board](https://www.figma.com/board/JluDgNpnfYoTbMeOkq5mE7). Overview arrows summarize navigation; the event tables below define behavior when conditions overlap.

## Decisions and boundaries

- A channel selection is an explicit watch-live action. Provider, group, filter, focus, details, favorite, hide and reorder actions never tune.
- Selecting a different channel B replaces A immediately. Cancelling or failing B never silently restarts A.
- Expanding the mini player changes presentation only, including when paused or recovering. Selecting the same channel from a channel, Favorite or Recent item requests live playback; reuse the session when possible, otherwise restart that channel. Already-live playback need not be needlessly retuned.
- One logical playback session serves in-app surfaces. This does not require the same player instance to survive backgrounding.
- Ongoing-playback recovery and an explicit Stop action are review-driven additions to the first-build behavior. They were not fully specified by the original startup-recovery ticket.
- Startup and ongoing recovery have finite, documented attempt and elapsed-time budgets. Connecting, Buffering, Reconnecting, terminal failure and Stream ended are distinct visible conditions.
- Failure/recovery stays on its current surface. A mini-player error cannot take over the Guide or steal browsing focus.

## Browsing origin and focus

Capture the latest browsing origin whenever a Home/Guide channel selection or mini-player expansion enters full screen. Store destination, provider identity, collection/filter, query, channel identity and scroll context. Do not permanently bind Back to where the session first began.

When a channel is selected from the compact browser, its cancellation/failure return target is the Guide for that browser's provider and personal collection, focused on the selected channel or a safe fallback. Keep this explicit even though the previous channel has ended.

Restore the same surviving focusable item by identity, then the next item at that position, then the previous item. If the collection is empty, use an enabled group selector, Browse channels or Manage hidden items as appropriate. A decorative section heading is never the fallback. Asynchronous errors and metadata/catalog refreshes do not steal current focus.

The compact browser follows the playing provider. Global Guide restores the last browsed provider. The explicitly scoped action **All channels · Provider A** opens A's Guide and updates browsing context to A without tuning. If A plays while B is browsed, expanding A and then pressing Back restores B.

## Playback events

| Event | Condition | Resulting screen | Playback effect | Restored focus |
| --- | --- | --- | --- | --- |
| Select channel B | A is playing or paused; B differs | Full screen: Connecting B | End A and replace it with B. No automatic rollback to A. | Connecting surface; Cancel is reachable |
| B starts | Current request succeeds | Full screen: B | Only B plays. Add Recents after success. | Player surface / controls trigger |
| Cancel B | Bare full-screen start or switch attempt | Originating Home/Guide; no mini player | Cancel B and recovery. A stays ended. | Original provider, collection, query and item; safe fallback |
| B fails | Definitive error or finite budget exhausted | B failure: Retry B / Choose another | No active video. Do not restart A. | Retry B; error arrival never steals focus from another visible layer |
| Retry B | B failure surface | Connecting B on the same surface | New bounded attempt for B. | Current action / Cancel |
| Choose another | Start or ongoing-playback failure | Origin browser; if already browsing, stay there | Clear the failed request/session and remove its player. | Origin item or focusable fallback |
| Select mini player | Same session, including paused or recovering | Expand current player surface | No retune, seek, resume or new stream. | Player controls; capture current browser as latest return origin |
| Select same channel tile | Channel/Favorite/Recent item is selected | Full screen at live | Explicit watch-live action. Reuse and seek/resume if possible; restart if needed. | Player; capture current browser origin |
| Playing stalls | Temporary lack of media | Buffering on current full/mini surface | Bounded wait; one session. Do not treat intentional pause as failure. | Preserve current focus |
| Transient interruption persists | Recoverable failure / buffering limit | Reconnecting on that same surface | Finite recovery attempts and elapsed-time limit. | Preserve current focus; Stop remains reachable |
| Playback recovers | Current recovery succeeds | Same surface: Playing | Continue selected channel; no cross-channel fallback. | Preserve focus; no Guide takeover |
| Terminal / exhausted failure | Playback had already started | Actionable playback failure on current surface | End automatic retry. Offer Retry / Choose another / Stop. | Preserve browsing focus; error actions reachable in mini player |
| Stream ends | End-of-stream event, not buffering | Stream ended on current surface | No endless automatic restart. Offer Watch live again / Choose another / Stop. | Preserve current focus |
| Pause window expires | Old live position no longer valid | Current player explains position unavailable | Offer Return to live. Never promise the old position is retained. | Current control or Return to live if its old control vanished |

The startup diagram is an overview, not the whole playback lifecycle. After playback begins the path is **Playing → Buffering → Reconnecting → Playing or actionable failure**, with bounded waiting and retry. Recoverable errors may go directly to Reconnecting. A terminal error can go directly to failure. A true end-of-stream goes to Stream ended. Pause/suspension is not inferred to be a failure from a generic “not playing” signal.

## Back precedence and Stop

Apply the first matching Back rule. An open layer wins over pending playback cancellation. The bare full-screen start rule covers initial starts, channel replacement, manual Retry/Watch-live attempts and their failure screens; it does not apply to ongoing recovery of an established session while the viewer is browsing.

| Event / precedence | Condition | Resulting screen | Playback effect | Restored focus |
| --- | --- | --- | --- | --- |
| 1. Back | Keyboard, channel-action, track or details layer open | Dismiss only topmost interaction layer | No cancellation or retune of underlying session/request | Trigger for that layer, or focusable fallback |
| 2. Back | Controls or compact browser open, even during recovery | Underlying full-screen surface | Keep underlying request/session and its bounded recovery | Layer trigger |
| 3. Back | Bare full-screen initial start, channel-switch/manual-retry attempt, or its failure | Latest originating browser; no player | Cancel or clear the attempt/failure; no active video or rollback | Captured origin item / safe fallback |
| 4. Back | Bare full-screen established playback, ongoing recovery, paused, ended or failed session | Latest originating browser with current player state in mini | Minimize presentation; do not restart or cancel recovery | Latest captured browser origin |
| 5. Back | Reorder move mode with no higher layer | Exit move mode; retain organization view | Cancel draft order; playback unchanged | Moved item at saved location / safe fallback |
| 6. Back | Home/Guide with mini or suspended player | Ordinary previous browsing destination | Never expand player as a Back side effect | Prior browsing location; repeated Back reaches app root |
| 7. Back | App root; no higher layer | TV launcher | Suspend and release as needed; no hidden audio or retry | System owns focus; no exit confirmation gate |
| Stop / Close player | Remote-reachable action in full-screen controls or mini-player actions, including pending/error states | Stay browsing, or return to latest browser from full screen; remove player | End playback, cancel all pending recovery, invalidate late results; no suspension resume prompt | Keep browsing focus, or origin/fallback when player held focus |

Stop is visible and reachable with the remote in player controls and mini-player actions, including Connecting, Reconnecting, failure and ended states. It clears the session and any suspended-resume context, while retaining browsing and saved Favorites/Recents. Stop is not Back, Pause or exit.

## Provider context and lifecycle

| Event | Condition | Resulting screen | Playback effect | Restored focus |
| --- | --- | --- | --- | --- |
| Choose provider / group / filter | Any browsing view | Selected provider/collection list | Never tune a channel | Selected control then reachable content |
| Global Guide | Last browsed provider is B; A may be playing | B Guide with B's saved query/collection | A remains unchanged in mini | B's saved focus |
| Expand A mini | Currently browsing B | A full screen; capture B as return origin | Same A session/state; no retune | Player controls |
| Back from A full screen | Entered by expanding A while browsing B | B with its exact saved context | A moves back to mini | B query, collection, item and scroll position |
| All channels · Provider A | Inside A's compact browser | A Guide; explicitly set browsed provider to A | A continues; scoped navigation does not tune | A's saved Guide context; playing A channel if no valid saved context |
| Open compact browser | A session exists | Favorites/Recents of A's provider | Keep A session/state | Saved browser item, current channel or focusable All channels action |
| App backgrounds | Any session or pending/recovery work | App is not visible | Suspend playback and retry work; release resources as needed | Retain enough context for warm return |
| Warm return | Process and return context survived | Restore prior surface with suspended status and explicit action | No autoplay. Resume only if old position remains valid; otherwise Watch live / Return to live. | Prior focus or enabled playback action if prior control disappeared |
| Fresh launch / process recreation | Runtime context is gone | Home without autoplay | No assumption that player survives. Recents contains successful viewing only. | Meaningful Home item or Browse channels |

A warm return is distinct from process recreation. With retained context, present an explicit playback action and validate any saved position before labeling it Resume. If the resource or live window is unavailable, use Watch live / Return to live. No background retry or audio continues. Returning with no prior session restores browsing without inventing a suspended player.

## Favorites, unavailable channels and visibility

Visible **Channel actions** are reachable alongside channel browsing using the D-pad; long press is not the only entry. Selecting the channel body remains direct watch-live. Action success is shown with the changed state and brief feedback without stealing focus.

| Task | Entry and action sequence | Completion feedback | Cancel / Back | Focus and playback |
| --- | --- | --- | --- | --- |
| Favorite | Focus channel → visible Channel actions → Add favorite | Favorite state updates in Home and Guide; small confirmation | Dismiss menu before selection makes no change | Return to same channel; no tune |
| Unfavorite | Focus favorite → Channel actions → Remove favorite | Saved flag clears; item leaves Favorites | Menu dismissal before action makes no change | Next item at same position, then previous; if empty, Browse channels. Playback unchanged |
| Unavailable favorite | Saved channel disappears after valid refresh → show retained Unavailable item | Preserve provider/channel identity; no guessed substitute | Back returns to prior collection | Item remains focusable; Refresh lineup or Remove favorite is reachable; selection never tunes another channel |
| Hide channel / group | Channel actions or Guide → Organize → choose item → Hide | Exclude it from ordinary Home/Guide/search/browser lists | Dismiss action menu before selection makes no change | Next/previous surviving item; if empty, Manage hidden items. Active playback continues |
| Restore hidden | Guide → Organize → Manage hidden items → choose item → Restore | Saved favorite/history/order retained; eligible entries reappear | Back returns to organization; committed restores remain | Next hidden item, previous, then Back to channels; playback unchanged |
| Empty after hiding | Ordinary view has no eligible items → Manage hidden items | Management remains reachable even with an empty lineup view | Back follows normal navigation | Focus Manage hidden items; never a decorative heading |
| Ungrouped channels | Guide → All channels or Ungrouped → select channel | Channels without usable group metadata remain discoverable | Back restores group/filter control | Group selection never tunes. Only channel selection watches live |

An unavailable saved channel and a hidden channel are different: disappearance preserves an unavailable identity; hiding intentionally filters ordinary lists but retains saved data. Neither is equivalent to no Favorites. The Guide includes All channels and an Ungrouped route so missing group metadata cannot hide playable channels.

## Organization, tracks and details

| Task / event | Entry and action sequence | Completion feedback | Cancel / Back | Focus and playback |
| --- | --- | --- | --- | --- |
| Enter move mode | Guide → Organize → Groups or Channels → item → Move | Mark moving item and show Finish / Cancel | Back cancels move mode before leaving organization | Keep focus on moving item; no tune |
| Move and finish | D-pad changes position → Finish | Commit provider-scoped order atomically | Cancel discards draft order | Keep focus by moved item's stable identity |
| Catalog refresh during move | Hold visual snapshot and queue update → Finish or Cancel → reconcile | Preserve draft order for surviving identities; append new items in provider order | Cancel applies last saved order to refreshed identities | If moved item vanished, cancel draft, explain change and choose surviving item/control |
| Lists using custom order | Apply saved group/channel order to Guide, All/Ungrouped, Favorites, favorite browser sections and channel-name search | Same provider identity has consistent relative order | Changing ordering has no playback effect | Recents and recent-browser sections remain chronological; custom order never rewrites history |
| Track selection | Player controls → Audio or Subtitles → available option | Apply available track; return to its control | Back closes only track menu | Return to Audio/Subtitles trigger; maintain session |
| Program details | Channel actions or player controls → Details | Open optional details without tuning; missing/invalid/stale state is explicit | Back closes details only | Return to originating item or Details trigger |
| Stale program information | Listing expired, invalid, missing or untrusted | Keep channel usable; do not label stale data as current or show fabricated progress | Details dismissal does not tune | Retain focus through metadata updates; thresholds/copy resolved inside first build |

Within each provider, flatten the ordered groups and their ordered channels to obtain a stable lineup order; ungrouped channels remain reachable and have deterministic placement. Project that order into matching channel lists. Recents always reflects viewing chronology.

A move is a draft. Finish commits atomically; Cancel/Back discards it. During a move, queue catalog reconciliation rather than moving items beneath the remote focus. After Finish/Cancel, reconcile stable identities; append genuinely new items in provider order. If the moved identity disappears, cancel the draft with feedback and restore a surviving focus target. Hiding, reordering and refresh never stop the playing channel.

Details are a separate action from channel playback. Missing, invalid, expired or stale information is represented honestly. Data known to be stale must not be labeled as the current program or shown as a current progress bar. Exact freshness policy, fallback copy and timing are unresolved first-build details, not deferred release scope.

## Provider setup outcomes

| Provider outcome | Visible result | Next actions | Data rule | Focus |
| --- | --- | --- | --- | --- |
| Invalid credentials | Connection rejected / check details | Edit details; try another provider | Do not save as a successful connection or echo secrets | Correction action / relevant field |
| Unreachable service | Cannot reach provider | Retry; edit address; choose another | Keep last valid saved lineup; do not relabel as empty | Retry or current browsing focus on background refresh |
| Malformed response | Provider response could not be read | Retry; edit connection; choose another | Do not overwrite valid cached catalog with bad data | Actionable recovery control |
| Valid empty lineup | Connection works; no channels returned | Refresh; edit connection; choose another | Distinguish successful empty result from network/auth/parse failure | Refresh / provider selector |

## First-build details still to settle or tune

- Exact startup, buffering and reconnection attempt/time budgets and recoverable-error classification; finite limits and the visible states above are required.
- Program-information freshness rules and copy; basic Details entry and top-layer dismissal are required now.
- Physical D-pad mapping and placement: OK for controls and Down for compact browsing remain testable proposals. Essential actions must also have visible remote-reachable controls.
- TV model/OS, representative stream capabilities and real-device validation.

These items must be resolved and demonstrated for first-build acceptance; they are not later-release exceptions.

## Later release work

QR phone setup and relay; schedule-grid presentation; trial/purchase eligibility, offline entitlement, expiry and restoration; broader platform/store qualification. Basic Details and missing/stale information handling are already first-build work.

## Ticket ownership

- 02: distinct provider outcomes and valid cache preservation.
- 03–05: personal actions, watch-live selection, group/search separation and ungrouped access.
- 06: initial/channel-switch and ongoing-playback recovery, replacement/cancellation and finite budgets.
- 07–09: provider-scoped navigation, latest return origin, Back precedence, Stop, mini-player recovery and suspension.
- 10–13: hide/restore, move-mode transactions, capabilities/tracks and basic Details.
- 14: integrated qualification, including failures after playback starts and warm versus cold return.

Ticket 09 now depends on 06 because mini-player recovery and cancellation must integrate the shared recovery behavior. The direct 06 → 14 edge is redundant through 09 and its dependents; 14 remains transitively blocked by 06. There are still 14 tickets and none is resolved.

## Platform evidence

The distinction between buffering, ended and error follows [Media3 player events](https://developer.android.com/media/media3/exoplayer/listening-to-player-events); “not playing” alone does not identify the cause. Application-level Connecting/Reconnecting and the budgets above remain product behavior to implement and validate.

Media3 recommends [releasing a player when it is no longer needed](https://developer.android.com/media/media3/exoplayer/hello-world#release-the-player). The design therefore promises preserved context across suspension, not survival of a particular player instance or live position. The implementation must choose the correct lifecycle boundary for its ownership model.

The app-root rule follows [Android TV navigation guidance](https://developer.android.com/training/tv/get-started/navigation#back-button-navigation): Back reaches the system without confirmation gates or navigation loops. It does not turn Stop into an app exit action.
