---
description: >-
  A sign request in Xumm is a prompt to approve a transaction or action on the
  XRP Ledger. This page will show you how you can create a Sign Request, and how
  you can deliver the request to the end user.
---

# Backend

When creating Sign Requests from a backend environment, the Xumm SDK is called with your API Key & Secret. A payload can be opened by any user. A user will not get notified about a payload, unless if they interacted with the payload through a **deeplink** or scanning the **Payload QR code**.

If you want to deliver backend created Sign Requests to a user & the user is identified by your application, you have to provide a `user_token` to the payload. The `user_token` can be obtained after the user interacted with your application & signed a payload. See: [push.md](../../../concepts/payloads-sign-requests/delivery/push.md "mention")

{% hint style="info" %}
For more information about the object contents to be used for Payloads & the return URL replacement variables, see: [https://xumm.readme.io/reference/post-payload](https://xumm.readme.io/reference/post-payload)
{% endhint %}

```typescript
import { Xumm } from "xumm"

const xumm = new Xumm("some-api-key", "some-secret-key")

const payload = await xumm.payload?.create({
  user_token: "xxxxxxxxxx",
  txjson: {
    TransactionType: "SignIn"
  },
  options: {
    return_url: {
      app: "https://sample.test/?...",
      web: "https://sample.test/?id={id}"
    },
    force_network: "MAINNET"
  },
  custom_meta: {
    identifier: "123123",
    instruction: "Please sign this to..."
  }
})) 
```

{% hint style="info" %}
To decide where the user is sent after signing the payload, please read:\
[payload-return-url.md](../../../concepts/payloads-sign-requests/payload-return-url.md "mention")
{% endhint %}
