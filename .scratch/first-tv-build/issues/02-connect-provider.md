# 02 — Connect a provider and watch its channels without guide data

**What to build:** Enter a provider's Xtream Codes details on the TV, save the connection, browse its channels, and select one to watch even when no program listings exist.

**Blocked by:** 01 — Play a test channel in an installable TV build

**Status:** ready-for-agent

**Type:** task

- [ ] Server address, username, and password can be entered and corrected with the TV remote; no separate app account is required.
- [ ] A successful connection saves credentials using appropriate platform protection and persists a validated channel lineup with stable provider-scoped identity.
- [ ] A channel can be selected and played without titles, broadcast times, artwork, or an EPG request completing.
- [ ] Invalid credentials, unreachable service, malformed responses, and a valid empty lineup produce distinct usable outcomes without disclosing credentials or credential-bearing playback URLs.
- [ ] Reopening the app restores the saved connection and last valid catalog; a failed refresh does not erase saved data or block access to the cached browsing view.
- [ ] Integration coverage exercises the setup-to-play path and missing-guide/failure cases against controlled provider responses.
