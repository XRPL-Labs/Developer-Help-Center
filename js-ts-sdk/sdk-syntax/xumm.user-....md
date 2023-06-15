---
description: Returns information about the signed in user (in case of xApp or Web3 flow).
---

# Xumm.user { ... }

{% hint style="info" %}
This method only applies to the xApp & Web3 (browser) flow. Backend flows (using API Key & API Secret) have no user context.
{% endhint %}

The following properties are part of the `user` object. Every property is a `Promise` that is resolved when the user is signed in.

* `account` - r-address
* `picture` - Profile picture or Hashicon URL
* `name` - Account name (if present) - e.g. Xumm Pro account name
* `domain` - Domain name (if present) for account
* `source` - Information source (e.g. a specific explorer)
* `networkType` - Enum, e.g. MAINNET, TESTNET, ... the user is connected to
* `networkEndpoint` - WebSocket endpoint to connect to the network
* `blocked` - If the account is on a blacklist (e.g. because of scams)
* `kycApproved` - If the account owner went through opt in KYC with Xumm
* `proSubscription` - If the account has a Xumm Pro subscription
* `profile` - Xumm Pro Profile slug (URL)
* `token` - User Token for future sign request Push delivery

The `token` field contains a `user_token`; this token is specific to both the application (SDK) credentials and the end user. It grants you access to asynchronously send [push.md](../../concepts/payloads-sign-requests/delivery/push.md "mention") notifications to the end user (for 30 days, unless granted long living tokens).

When your application creates a payload for the end user to sign using the SDK session (or JWT), a user will always receive a push notification.

If you want to asynchronously create a payload on your backend using the [backend-sdk-api.md](../../environments/backend-sdk-api.md "mention")flow, you can include this `token` in the `user_token` field of the payload.
