# 05 — Browse groups and search channel names

**What to build:** Navigate the provider's groups or search channel names to find and play a channel without relying on program metadata.

**Blocked by:** 02 — Connect a provider and watch its channels without guide data

**Status:** ready-for-agent

**Type:** task

- [ ] The provider's channel groups are preserved, with remote-reachable All channels and Ungrouped routes for channels lacking usable group metadata.
- [ ] Channel-name search works within the selected provider and can be entered, cleared, and exited with the remote.
- [ ] Selecting a group displays its channels without changing playback. Selecting a channel item, including a channel-name search result, starts that channel.
- [ ] Selecting providers, filters, groups, or moving focus makes no playback request; duplicate display names do not collapse distinct channel identities.
- [ ] Large controlled catalogs use bounded rendering and remain navigable without loading program-guide data first.
- [ ] Empty groups, no search results, missing logos, and unavailable listings have readable states with reachable next actions.
- [ ] Tests cover group navigation, search results, duplicate names, missing data, and remote selection through to playback.
