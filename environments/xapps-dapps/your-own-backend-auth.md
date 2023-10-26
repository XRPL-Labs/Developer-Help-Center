---
description: >-
  Xumm xApps yield a JWT that can be used to make subsequent calls from the user
  context to the Xumm API's. You can also use this JWT for your own backend.
---

# Your own backend (Auth)

{% hint style="info" %}
If you want to identify a Xumm xApp user with your own backend, you can rely on the xApp JWT's issued by Xumm: the **secret used to sign the JWT is your own Xumm application secret** (HMAC, HS256).
{% endhint %}

This makes it really convenient to obtain three things at once, making calls to your own backend with an `Autorization: Bearer {The Xumm JWT}` header:

1. You obtain basic user information, like the r-address and network the user is connected to, as this information is encoded in the JWT.
2. You can verify the authenticity of the JWT, as it is signed with your own Xumm API Secret.
3. You can make calls from the user context to the Xumm backend with this JWT (for as long as it is valid: 24h).

Every time when a user opens your xApp, a new JWT is issued, valid for 24h.

{% hint style="success" %}
Please note: if you are using the OAuth2 flow instead of an xApp to obtain your JWT, you can verify the OAuth2 issued RS256 JWT using the certificate info publised as per OpenID specifications: [https://oauth2.xumm.app/certs](https://oauth2.xumm.app/certs)
{% endhint %}

### How to validate a JWT

When using the JWT for authorization, you need to validate it before you can make sure that the user is who they say they are. This is a brief explanation in how to verify the JWT using a npm package called [`jsonwebtoken`](https://www.npmjs.com/package/jsonwebtoken) and the bearer provided by the Xumm SDK.

You can obtain the JWT associated with the OTT by initiating the Xumm SDK:

```
const xumm = new Xumm(apiKey, xAppToken)
```

Then get the bearer by awaiting the environment:

```
const bearer = await xumm.environment.bearer
```

{% hint style="danger" %}
**This bearer is the JWT. You must check if the JWT is valid.**
{% endhint %}

First, run:

```
npm install jsonwebtoken
```

After this, use the code underneath to verify the JWT. You'll need the xApp API Secret to sign the JWT and check it's validity.

This xApp API Secret is found in the developer console at [https://apps.xumm.dev](https://apps.xumm.dev).

```javascript
const jwt = require('jsonwebtoken')

const apiKey = '' // Your Xumm API key here
const apiSecret = '' // Your Xumm API secret (BACKEND ONLY!)
const bearer = await xumm.environment.bearer

try {
  // If decoded comes back as an object, the JWT is valid.
  // Otherwise, the catch block is activated
  const decoded = jwt.verify(bearer, apiSecret);

  // For extra security, check if the decoded JWT contains
  // the client_id of your xApp, e.g. the API Key from the developer console  
  if(decoded.client_id === apiKey) {
    // JWT is valid and signed for this client (client_id matched)
  } else {
    // Valid JWT, but for another client? There's something
    // wrong with an otherwise valid JWT.
  }
} catch (error) {
  // Handle your error here and inform the user that their access is denied.
}
```
