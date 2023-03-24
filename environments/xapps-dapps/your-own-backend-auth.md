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
