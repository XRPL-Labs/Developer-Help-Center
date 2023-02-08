---
description: ...
---

# 🔐 Authorization & Credentials

## Authorization

...

## Credentials

|                                                                             | Backend                                                                                                                                 | PKCE / JWT                                              | xApps                                                                     |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------- |
| <mark style="color:blue;">Also known as</mark>                              | "Server side"                                                                                                                           | "Sign in with Xumm"                                     | "dApps", "web apps" embedded in Xumm                                      |
| <mark style="color:blue;">Credentials</mark>                                | API Key & Secret                                                                                                                        | JWT (SDK handles this for you)                          | JWT (SDK handles this for you)                                            |
| <mark style="color:blue;">Credential source</mark>                          | Obtained from the [Xumm Developer Dashboard](https://apps.xumm.dev)                                                                     | Obtained after end user logs in (SDK does this for you) | Automatically obtained through a "One Time Token" (SDK does this for you) |
| <mark style="color:blue;">Can send sign request push notifications</mark>   | After the user signs their first [Sign Request](payloads-sign-requests/) by you through deeplink / QR with a then obtained "User Token" | Yes                                                     | Yes                                                                       |
| <mark style="color:blue;">User identified with credentials?</mark>          | No, ["SignIn" payload](../environments/backend-sdk-api/user-identification-payloads.md) (Sign Request) required first.                  | Yes                                                     | Yes                                                                       |
| <mark style="color:blue;">Usable in backend environments?</mark>            | Yes                                                                                                                                     | Yes (but frontend obtained)                             | Yes (but frontend (xApp) obtained)                                        |
| <mark style="color:blue;">Usable in frontend (browser) environments?</mark> | No                                                                                                                                      | Yes                                                     | No                                                                        |
| <mark style="color:blue;">CORS ready?</mark>                                | No                                                                                                                                      | Yes (JWT endpoints, SDK handles this for you)           | Yes (JWT endpoints, SDK handles this for you)                             |
| <mark style="color:blue;">Usable in native app environments?</mark>         | No                                                                                                                                      | Yes (but OAuth2 sign in flow required)                  | No                                                                        |
