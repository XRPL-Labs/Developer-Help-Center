---
description: >-
  When building a native app (iOS / Android / React Native / Capacitor / ...)
  you can leverage "Sign In with Xumm" and offloading transaction signing to
  Xumm as well. This uses application deep links.
---

# Native Apps

The process to integrate Sign In with Xumm and transaction signing by Xumm with your own native app is actually quite similar to **either** the [browser-web3](browser-web3/ "mention")flow: it uses OAuth2 (PKCE or Implicit flow) or the [backend-sdk-api.md](backend-sdk-api.md "mention")flow.

Combined with "Deep Links", your application sending off the user to Xumm will happen with a simple app-redirect. After the user interacted with your sign request, Xumm will return the user to the Return URL: the URL you added to your sign request payload to be opened post-signing.

If your application registers a Deep Link URL as well, and you pass that URL to Xumm as the payload Return URL, the user will be redirected back to your app. To match state, you can add information to the Deep Link URL Xumm sends the user to.

## Integration

### Sign In only

If you just want to authorize/identify a user with his/her r-address, the **OAuth2 "Identify" flow** suffices: you send off the user to a Sign In URL with a return URL and the user will return to your application with a **JWT (JSON Web Token)** you can use to call the Xumm API to get the user identification information (r-address). For more information, see [identity-oauth2-openid](identity-oauth2-openid/ "mention").

### Sign In & Sign Requests

If you also want to send Sign Requests to users & you don't want the user to re-authorize the JWT every 24h, you can generate Sign Requests yourself, in which case the flow you will use is the [backend-sdk-api.md](backend-sdk-api.md "mention")flow. You craft your **Sign In Payload:** [user-identification-payloads.md](backend-sdk-api/user-identification-payloads.md "mention") yourself, obtain a **User Token** after which you can generate user bound sign requests.

This workflow requires a backend on your end, where our application communicates to your backend to generate the Sign Requests. You need a backend for this, as you do not want to expose your Xumm API keys in your compiled application.

{% hint style="info" %}
Please **do not** include your Xumm API Secret in your native app build. Native apps can be decompiled and you do not want your API Secret to be abused by third parties.
{% endhint %}
