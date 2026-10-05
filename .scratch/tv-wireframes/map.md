# TV wireframes

## Notes

Current design: [Better IPTV — TV wireframes](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-4), page **01 · Revised Home and Guide**. The user rejected the original generic list/card direction; that page is retained as **99 · Superseded first pass**, not as the implementation target.

These are editable grayscale design frames, not app code or a functioning remote-control prototype. Station names, wordmark blocks, program titles and times are illustrative fixtures. The [interaction contract](../first-tv-build/interaction-contract.md) remains authoritative for behavior. No implementation ticket was resolved or given a design prerequisite.

## Decisions-so-far

- Visually inspected official Fubo, Sling and YouTube TV guide assets, plus Fubo/Sling Home and Favorites assets. Sources and device/date limits are in [the visual research note](../product-discovery/research-tv-guide-visuals.md). A current YouTube TV Home layout was not verified and is not claimed as a design source.
- Home uses station shelves with a selected-channel context region. Favorites lead and Recents follows. Missing program data does not turn the screen into repeated error messages or require artwork.
- Guide uses an aligned channel rail and a compact browsing area with seven visible channel rows. A selected-item context region sits above it. Personal collections and provider groups are directly reachable.
- A small options target appears for the focused item, opening a side sheet. Permanent Actions buttons on every channel were removed.
- Existing playback uses the upper-right context region, preserving the full width of the browsing area. It is the active session, not an automatically tuned preview. The playing provider remains distinct from the browsed provider.
- R03 and R04 show partial and absent program data. R07 illustrates the later schedule-grid presentation with sample reliable EPG; it does not move the grid into the first-build scope.
- The wireframes preserve quiet launch, explicit channel selection and the existing Back/Stop/session contract. Bare-player physical mapping remains a proposal: OK plays/pauses when supported, Up reveals controls, Down opens the browser. Visible menu focus changes what OK activates.

| Frame | Review link | Purpose |
| --- | --- | --- |
| R01 | [Home](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-4) | Favorites and Recents without autoplay |
| R02 | [All favorites](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-8) | Station-focused favorite browsing |
| R03 | [Partial guide data](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-12) | Supplied program titles mixed with playable channel fallbacks |
| R04 | [No guide data](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-16) | Channel access without fake time slots |
| R05 | [Different browsed and playing providers](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-20) | Harbor lineup, Northline playback |
| R06 | [Channel options](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-24) | Contextual favorite/hide/details actions |
| R07 | [Schedule grid, later release](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-28) | Future reliable-EPG presentation |
| R08 | [Home with active playback](https://www.figma.com/design/8NLSKwfoBAVNf20N52MwBo?node-id=15-32) | Same shelves plus the existing player |

## Fog

- This focused redraw is a reviewable visual direction, not a claim that the user has accepted it. The remaining first-pass setup, management and playback-state frames have not yet been restyled to it.
- Actual station logos/artwork, brand identity and final visual polish remain open. Wordmark blocks represent provider channel identity, not verified provider assets.
- Couch-distance text, long channel names, D-pad reachability, focus transfer to the options target/player, scrolling and Back precedence need an interactive prototype and physical-TV testing. Static frames do not validate these.
- Missing/empty collections, unavailable favorites, all-hidden recovery, search keyboard/no-results and all recovery variants still need a complete revised visual-state pass after the direction is settled.
- Numerical recovery budgets and program freshness rules remain first-build requirements to resolve and test.
