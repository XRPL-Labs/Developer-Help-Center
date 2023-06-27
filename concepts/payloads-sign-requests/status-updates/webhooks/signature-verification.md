---
description: >-
  Signature verification is crucial for ensuring the integrity and authenticity
  of the data received. It involves verifying that the data was sent by Xumm and
  has not been tampered with.
---

# Signature verification

If you want to make sure a WebHook received by your platform has been sent by the Xumm platform, verify the signature the platform sends in an HTTP header.

Every WebHook call contains a signature to verify the authenticity. It sends an HMAC using your application secret as a key. Sample verification in NodeJS:

```javascript
import crypto from 'crypto'

// Xumm App secret (Xumm developer console)
const secret = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

const timestamp = req.headers?.['x-xumm-request-timestamp'] || ''
const json = req.body

const hmac = crypto.createHmac('sha1', secret.replace('-', ''))
  .update(timestamp + JSON.stringify(json))
  .digest('hex')

console.log(hmac, hmac === req.headers?.['x-xumm-request-signature'])
```
