---
description: >-
  If you simply want to offer users a static link / QR code to sign a specific
  XRPL transaction, you can craft a link (to be offered directly or as contents
  of a QR code) for users to click / scan.
---

# Simple Sign Link/QR

Offering a direct link / QR code to a payload does **not** come with the advantages of creating a [payloads-sign-requests](concepts/payloads-sign-requests/ "mention") of getting live feedback & webhooks based on the user's engagement.

The advantage of a simple Sign Link / QR is that you can craft the link / QR once, and it will be available for all users without further code implementations.

Simple Sign Link/QR is available for the following transaction type(s)

* `TrustSet` (adding a Trust Line, a.k.a. adding a Token)

## Crafting the link / QR contents

```javascript
const tx = {
  TransactionType: 'TrustSet',
  Flags: 131072,
  LimitAmount: {
    currency: 'XAH',
    issuer: 'rswh1fvyLqHizBS2awu1vs6QcmwTBd9qiv',
    value: '100000000',
  }
}

const str = JSON.stringify(tx)
const hex = Buffer.from(str, 'utf-8').toString('hex')

console.log(`https://xaman.app/detect/${hex}`)
```

Example QR:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

