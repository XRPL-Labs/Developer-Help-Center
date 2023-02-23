---
description: >-
  A sign request in Xumm is a prompt to approve a transaction or action on the
  XRP Ledger. This page will show you how you can create a Sign Request, and how
  you can deliver the request to the end user.
---

# Backend

When creating Sign Requests from a backend environment, the Xumm SDK is called with your API Key & Secret. A payload can be opened by any user. A user will not get notified about a payload, unless if they interacted with the payload through a **deeplink** or scanning the **Payload QR code**.

If you want to deliver backend created Sign Requests to a user & the user is identified by your application, you have to provide a `user_token` to the payload. The `user_token` can be obtained after the user interacted with your application & signed a payload. See: [push.md](../../../concepts/payloads-sign-requests/delivery/push.md "mention")

```typescript
import { Xumm } from "xumm"

const xumm = new Xumm("some-api-key", "some-secret-key")

const payload = await xumm.payload?.create({
  user_token: 'xxxx',
  txjson: {
    TransactionType: 'SignIn'
  }
})) 
```
