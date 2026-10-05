# Phone-to-TV provider setup

Researched: 2026-10-04. Proposals, not a selected transport or approved cryptographic design. No device, browser, network, or credentials were tested. The [working spec](./spec.md) requires QR phone setup and direct TV entry; [ADR 0002](../../docs/adr/0002-device-owns-personalization.md) keeps personalization local without an app account.

**Recommendation:** investigate an accountless, short-lived HTTPS relay with credentials encrypted from phone to TV as the first public-release candidate. It avoids requiring browser access to the TV's LAN address. This adds a small operated service; it does not require cloud profiles or persistent cloud credential storage. LAN-only remains feasible, but should not be presented as a trivial or automatically safer option.

## Architecture comparison

| Option | Intended flow | Main tradeoff |
| --- | --- | --- |
| Direct LAN | QR identifies a temporary TV endpoint; the phone opens a form and sends details directly. | No relay, but requires LAN reachability plus a trustworthy way to deliver the form and protect credentials. |
| HTTPS page and encrypted relay | QR pairs the browser with one temporary TV session; encrypted details pass through a relay, and the TV retrieves/decrypts them. | Works without phone-to-TV LAN routing; depends on internet, hosted code, service availability, and correct pairing/encryption. |
| Platform phone keyboard | Viewer pairs the Google TV or Fire TV mobile remote, then types into the TV app's fields. | Simplifies direct entry, but requires another app and does not itself deliver the requested QR web form. |

These are proposed flows. The constraints below determine feasibility.

## Why LAN-only is not simple

Android can advertise a local service using DNS-SD and run a listening socket. A QR can carry its address directly; discovery is not the same as secure transport. [Android NSD](https://developer.android.com/develop/connectivity/wifi/use-nsd). Both devices still need a network path: access-point/client isolation can prevent device communication even when devices have internet access. [Google's isolation guidance](https://support.google.com/chromecast/answer/7566322?hl=en-CA).

The strongest problem is **trustworthy browser code delivery**. Opening `http://192.168.x.x` as a top-level page is different from an HTTPS page fetching HTTP resources, but it remains an insecure origin. The secure-context exception for `localhost`/loopback refers to the phone itself, not another device on its LAN. Browser `SubtleCrypto` requires a secure context; using a JavaScript crypto library would not protect form code delivered over modifiable HTTP. [Secure Contexts](https://www.w3.org/TR/secure-contexts/), [Web Crypto API and security considerations](https://www.w3.org/TR/webcrypto/).

Moving the form to hosted HTTPS solves code-delivery transport, but its requests to local HTTP encounter mixed-content and cross-origin restrictions. Chrome 142 introduced permission-gated local-network access from secure contexts, including a mixed-content exemption for qualifying local requests. This is a versioned browser feature, not a universal exemption; granting permission also does not encrypt HTTP traffic. [Mixed Content](https://www.w3.org/TR/mixed-content/), [Chrome 142](https://developer.chrome.com/release-notes/142), [Chrome implementation details](https://developer.chrome.com/blog/local-network-access).

Safari/iOS needs separate qualification. Apple's technical note exempts Safari traffic from the OS-level local-network permission; that does not remove web security rules. WebKit's tracker shows local-network enforcement work landing in September/October 2026, which does not establish a shipping Safari compatibility guarantee. [Apple TN3179](https://developer.apple.com/documentation/technotes/tn3179-understanding-local-network-privacy), [WebKit implementation tracking](https://bugs.webkit.org/show_bug.cgi?id=250607), [October change](https://bugs.webkit.org/show_bug.cgi?id=325552).

Local HTTPS needs trusted certificates and a lifecycle for names/keys. Self-signed certificates are not automatically trusted; distributing one shared certificate private key inside every TV app is unsafe. [Let's Encrypt guidance](https://letsencrypt.org/docs/certificates-for-localhost/). Android 17 also requires local-network permission for target-SDK-37 apps, including accepting incoming TCP; older TV/Fire OS behavior must be checked separately. [Android local-network permission](https://developer.android.com/privacy-and-security/local-network-permission).

## What an encrypted relay would commit us to

Proposed boundary: the TV creates a temporary pairing session; the QR binds the phone to that session and the intended TV. The browser encrypts provider details before upload; only the intended TV holds the required decryption material. Both communicate outward over HTTPS. The relay retains ciphertext only until delivery or expiry; successful setup ends the session. Favorites/history never enter this flow.

That describes a goal, not a vetted protocol. Use established cryptographic constructions and reviewed implementations. For example, HPKE defines recipient-public-key encryption, but explicitly does not supply replay prevention or a complete application protocol. Session binding, correct-TV confirmation, single use, expiry, and retry handling still require design and review. [RFC 9180](https://www.rfc-editor.org/rfc/rfc9180).

The QR/code, expiration, and bounded-polling pattern has a standards precedent in OAuth device authorization. Its account-based authorization grant is **not** an automatic solution for transferring arbitrary Xtream credentials; we would borrow interaction principles, not claim provider OAuth support. [RFC 8628](https://www.rfc-editor.org/rfc/rfc8628).

Temporary ciphertext is different from a persistent cloud credential vault, but it remains server-held data. Proposed operational requirements include TTL enforcement, deletion after completion, abuse limits, availability monitoring, and preventing payloads/secrets from entering logs, analytics, or backups. The hosted page remains trusted: compromised delivered JavaScript can capture credentials before encryption. End-to-end relay encryption cannot honestly promise protection from that. [Web Crypto security model](https://www.w3.org/TR/webcrypto/).

## Simpler fallback and decision boundary

Google documents using a phone keyboard for TV text/password entry; Amazon's Fire TV app similarly provides a keyboard after device pairing on the same Wi-Fi. These can improve the agreed TV-entry path, subject to testing our fields. They are not evidence of a reusable third-party QR setup API. Google's own device-setup QR flow is device onboarding, not provider setup inside our app. [Google phone keyboard](https://support.google.com/chromecast/answer/11221499?hl=en), [Google TV app](https://blog.google/products-and-platforms/platforms/google-tv/seven-app-tips/), [Amazon mobile remote](https://digprjsurvey.amazon.com/csad/help/node/TtsAzTRhSQ38wfm2D7), [Google device setup](https://support.google.com/googletv/answer/10050221?hl=en).

The user decision is whether operating a temporary setup service is acceptable—not whether to create app accounts. Before committing to a mechanism, validate iPhone Safari/Android Chrome, TV network changes, isolated Wi-Fi, expiry/replay/wrong-TV cases, interruption and retry, and browser/app key handling. Keep direct TV entry available. No host, new account, crypto suite, or infrastructure has been selected.
