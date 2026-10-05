---
status: accepted
---

# Temporary encrypted relay for phone setup

Use an accountless, short-lived HTTPS relay for phone setup so the phone browser does not need a direct network path to the TV. The intended design encrypts provider details for the selected TV before upload, retains only temporary ciphertext at the relay, and removes it after delivery or expiry. Direct TV entry and normal viewing remain independent of the setup relay, while favorites/history stay on the device as established in ADR 0002.

## Consequences

This adds an operated service, but does not select a hosting vendor, cryptographic construction, or completed pairing protocol. Correct-TV binding, single use, expiry, retry behavior, and deletion require explicit design and validation. The hosted setup page is trusted code; encrypting relay messages does not protect credentials from a compromised page that captures them before encryption.

The [phone setup research](../../.scratch/product-discovery/research-phone-setup.md) records the browser/network tradeoffs and evidence. No service has been deployed.
