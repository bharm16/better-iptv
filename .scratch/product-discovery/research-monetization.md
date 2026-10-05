# Google Play monetization boundaries

Research date: 2026-10-04. Product-discovery evidence for the first Google Play release; no business model, price, trial duration, or billing implementation is selected. An app account and cloud profile synchronization remain outside scope. The accepted temporary provider-setup relay does not itself settle purchase verification architecture.

## Two different one-time payment models

**Paid download:** set a price for the app listing, so purchase precedes installation. Google allows changing a paid app to free, but once offered free, that listing cannot become paid; charging for the download would require a new app/package. This restriction concerns the download price. [Google Play app pricing](https://support.google.com/googleplay/android-developer/answer/6334373)

**Free download with a permanent unlock:** sell a non-consumable one-time product inside the app. Google describes these as a single purchase granting a permanent benefit associated with the user's account, such as a premium upgrade. This is distinct from converting the free download into a paid listing. [One-time products](https://developer.android.com/google/play/billing/one-time-products)

## Trial is a separate design decision

Google's documented free-trial pricing phase belongs to **subscription offers**. Current one-time-product documentation lists buy/rent options and preorder/discount offers; it does not document the same free-trial phase for a permanent unlock. [Subscription offers](https://support.google.com/googleplay/android-developer/answer/140504), [One-time purchase options and offers](https://developer.android.com/google/play/billing/one-time-product-multi-purchase-options-offers)

**Design inference:** a free download that allows temporary use before a one-time unlock needs app-managed trial eligibility and expiry. The later unlock is an explicit purchase, rather than an automatically renewing subscription. Trial start, offline behavior, reinstalls, and resets must be resolved separately; choosing a one-time purchase does not answer them.

## Purchase access and an accountless app

For in-app purchases, verify legitimacy before granting access and grant only once payment reaches `PURCHASED`, not while pending. Acknowledge completed purchases within three days or Play can refund and revoke them. Google strongly recommends secure-server verification; its documentation also provides client-side acknowledgement. This does not establish that a backend is unnecessary. [Billing integration](https://developer.android.com/google/play/billing/integrate)

The app should query Play purchases when connecting/returning to the foreground, covering missed callbacks and purchases from another device. Google's app-user identifiers are optional metadata. **Inference:** a Play purchase can underpin restored access without requiring a separate app login; purchase restoration and synchronization of favorites/history are different features. Do not rely exclusively on a local “unlocked” flag. [Purchase processing and identifiers](https://developer.android.com/google/play/billing/integrate)

The interview can choose free, one-time, or recurring payment now. What is included, trial behavior, offline access, refund handling, and any future entitlement sharing with another store remain subsequent product and implementation decisions. None has been exercised in Play Console or tested on a device.
