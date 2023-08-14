# Xumm.payload { ... }

Payloads are the primary reason for the XUMM API (thus this SDK) to exist.&#x20;

> An XRPL transaction "template" can be posted to the XUMM API. Your transaction tample to sign (so: your "sign request") will be persisted at the XUMM API backend. We now call it a a **Payload**. XUMM app user(s) can open the Payload (sign request) by scanning a QR code, opening deeplink or receiving push notification and resolve (reject or sign) on their own device.

A payload can contain an XRPL transaction template. Some properties may be omitted, as they will be added by the XUMM app when a user signs a transaction. A simple payload may look like this:

```javascript
{
  txjson: {
    TransactionType : 'Payment',
    Destination : 'rwiETSee2wMz3SBnAG8hkMsCgvGy9LWbZ1',
    Amount: '1337'
  }
}
```

As you can see the payload looks like a regular XRPL transaction, wrapped in an `txjson` object, omitting the mandatory `Account`, `Fee` and `Sequence` properties. They will be added containing the correct values when the payload is signed by an app user.

Optionally (besides `txjson`) a payload can contain these properties ([TS definition](https://github.com/XRPL-Labs/XUMM-SDK/blob/d2aae98eb8f496f4d77079c777aa41df754d4ebc/src/types/xumm-api/index.ts#L79)):

* `options` to define payload options like a return URL, expiration, etc.
* `custom_meta` to add metadata, user insruction, your own unique ID, ...
* `user_token` to push the payload to a user (after obtaining a user specific token)

A more complex payload [could look like this](https://gist.github.com/WietseWind/ecdfd58bece14e5d15e41138fa4b0f4a). A [reference for payload options & custom meta](https://xumm.readme.io/reference/post-payload) can be found in: [payloads-sign-requests](../../../concepts/payloads-sign-requests/ "mention")

Instead of providing a `txjson` transaction, a transaction formatted as HEX blob (string) can be provided in a `txblob` property.
