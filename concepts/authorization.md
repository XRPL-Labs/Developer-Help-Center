---
description: >-
  How to authorize when communicating with the Xumm platform depends on your
  workflow.
---

# 🔐 Authorization & Credentials

## Authorization

### Backend

When communicating with the Xumm platform from your backend environment, you will need a **API Key** and **API Secret**. They can be obtained from our [Developer Dashboard](https://apps.xumm.dev/), and are to be passed in the `x-api-key` and `x-api-secret` headers to our platform.

### Frontend (browser, client side)

[Frontend (browser, client side) implementations](../environments/browser-web3/) [browser-web3](../environments/browser-web3/ "mention") can use our [Javascript/Typescript SDK](https://www.npmjs.com/package/xumm), in which case the entire authorization is abstracted away. Under the hood, the user will go through an OAuth2-flow and a JWT (JSON Web Token) is obtained from our platform. This token is valid for 24 hours and user context bound.

If you are building your own frontend implementation, any OAuth2 (Implicit and PKCE flows both supported) client will do. See [identity-oauth2-openid](../environments/identity-oauth2-openid/ "mention")

{% hint style="danger" %}
**Never** use an API Secret obtained from the Developer Dashboard in a frontend environment! Anyone in possession of your API Secret (`x-api-secret`) can create payloads (Sign Requests) on behalf of your application. **If abused, this can immensely damage the reputation of your application.**&#x20;
{% endhint %}

### xApp

[xApps](../environments/xapps-dapps/) [xapps-dapps](../environments/xapps-dapps/ "mention") are loaded with several URL Query Paramters added, one of which is the `xAppToken` parameter. This parameter contains what we refer to as the "OTT", the "One Time Token". This token can be resolved by your application to a JSON response containing:

* user context information
* a JWT, JSON Web Token, allowing you to make subsequent calls to our platform

If you use our [Javascript/Typescript SDK](https://www.npmjs.com/package/xumm), this entire authorization flow is abstracted away by our SDK; the SDK (in the xApp, client side) will automatically resolve the xApp Token ("OTT") and use the JWT to make subsequent calls to our platform.

### Native application

Any OAuth2 (Implicit and PKCE flows both supported) client will do. [Your application](../environments/native-apps.md) [native-apps.md](../environments/native-apps.md "mention") can redirect the user to our platform (to be redirected to the Xumm app) to sign in after which the client will be redirected back to your application (if your application supports deep links). You will obtain a JWT (JSON Web Token) to communicate to our platform from the user context. See:[identity-oauth2-openid](../environments/identity-oauth2-openid/ "mention")

## Credentials

|                                                                             | Backend                                                                                                                                 | PKCE / JWT                                              | xApps                                                                     |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------- |
| <mark style="color:blue;">Also known as</mark>                              | "Server side"                                                                                                                           | "Sign in with Xumm"                                     | "dApps", "web apps" embedded in Xumm                                      |
| <mark style="color:blue;">Credentials</mark>                                | API Key & Secret                                                                                                                        | JWT (SDK handles this for you)                          | JWT (SDK handles this for you)                                            |
| <mark style="color:blue;">Credential source</mark>                          | Obtained from the [Xumm Developer Dashboard](https://apps.xumm.dev)                                                                     | Obtained after end user logs in (SDK does this for you) | Automatically obtained through a "One Time Token" (SDK does this for you) |
| <mark style="color:blue;">Can send sign request push notifications</mark>   | After the user signs their first [Sign Request](payloads-sign-requests/) by you through deeplink / QR with a then obtained "User Token" | ✅  Yes                                                  | ✅  Yes                                                                    |
| <mark style="color:blue;">User identified with credentials?</mark>          | No, ["SignIn" payload](../environments/backend-sdk-api/user-identification-payloads.md) (Sign Request) required first.                  | ✅  Yes                                                  | ✅  Yes                                                                    |
| <mark style="color:blue;">Usable in backend environments?</mark>            | ✅  Yes                                                                                                                                  | Yes (but frontend obtained)                             | Yes (but frontend (xApp) obtained)                                        |
| <mark style="color:blue;">Usable in frontend (browser) environments?</mark> | [❌](https://unicode-table.com/en/274C/) No                                                                                              | ✅  Yes                                                  | ✅  No                                                                     |
| <mark style="color:blue;">CORS ready?</mark>                                | [❌](https://unicode-table.com/en/274C/) No                                                                                              | Yes (JWT endpoints, SDK handles this for you)           | Yes (JWT endpoints, SDK handles this for you)                             |
| <mark style="color:blue;">Usable in native app environments?</mark>         | [❌](https://unicode-table.com/en/274C/) No                                                                                              | Yes (but OAuth2 sign in flow required)                  | [❌](https://unicode-table.com/en/274C/) No                                |

