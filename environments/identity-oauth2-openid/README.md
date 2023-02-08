---
description: >-
  The Xumm platform can act as the OAuth2 provider. The Xumm platform supports
  the OAuth2 / OpenID Connect flow. Authenticate and identify end users using
  their self custodial XRPL accounts.
---

# Identity (OAuth2, OpenID)

{% hint style="info" %}
All credentials created in the Xumm Developer Console ([https://apps.xumm.dev](https://apps.xumm.dev)) will work with the OAuth2 / OpenID Connect flow.
{% endhint %}

## OAuth2 flows

The Xumm OAuth2 / OpenID Connect provider supports the **authorization code** flow and the **implicit flow**.

The **PKCE flow** (which is the new & more secure industry standard and replaces the Implicit flow) is also available.&#x20;

All supported OAuth2 flows have their own use cases, advantages and caveats. The right one depends on your project & audience.

| Authorization code                                                                                                                                                      | PKCE                                                                                                                                                                                                     | Implicit                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Backend                                                                                                                                                                 | Frontend                                                                                                                                                                                                 | Frontend                                                                                                                                                 |
| API Key + Secret                                                                                                                                                        | API Key                                                                                                                                                                                                  | API Key                                                                                                                                                  |
| Custom implementation, custom sessions / token persistence if needed.                                                                                                   | Xumm SDK handles user sign in & session retrieval                                                                                                                                                        | Xumm SDK handles user sign in & session retrieval                                                                                                        |
| As secure as your own implementation                                                                                                                                    | Secure (Man in the Middle attack not possible)                                                                                                                                                           | Secure (but Man in the Middle attack possible)                                                                                                           |
| You deal with the **mobile** return flow state persistence. You will have to make sure you restore your session to cover sessions where user return in another browser. | Only works on **mobile** when users leave and return from & to the same browser. E.g. when starting off in a Twitter embedded browser frame & returning to the native OS browser, the sign in will fail. | Works on **mobile** even when users start in one browser and get redirected to another browser (e.g. the OS native browser). **Basically always works.** |
| You deal with the **desktop** sign in flow (redirect / popup / ...)                                                                                                     | Xumm SDK (TypeScript/Javascript) will trigger a pop up & handle sign state & events.                                                                                                                     | Xumm SDK (TypeScript/Javascript) will trigger a pop up & handle sign state & events.                                                                     |

## Credentials & Redirect URLs

To use the Xumm Platform as OAuth2 / OpenID Connect provider, one or more valid OAuth2 redirect URI's must be whitelisted in the [Xumm Developer Console](https://apps.xumm.dev/), on an application level.&#x20;

The same API Key and API Secret the Xumm Developer Console offers to be used calling our API's and using our SDK's can be used as OAuth2 client id and secret.

## Obtained credential (bearer)

The Xumm platform returns a Bearer token (JWT) with limited validity. The token can not be refreshed: after expiration a new user sign in is mandatory to obtain a new JWT token.

{% hint style="success" %}
When using the [**Xumm SDK**](https://www.npmjs.com/package/xumm) (TypeScript & Javascript) all OAuth2/JWT interaction, authorisation & implementation will be abstracted away, which is by far the easiest way to interact with the Xumm platform.
{% endhint %}

Building your own integration, or using a standard OAuth2 consumer? All JWT tokens obtained through from a Xumm OAuth2 flow can be used with the [JWT API endpoints](https://xumm.readme.io/reference/oauth2-jwt) (from a user locked context). The way to interact with the JWT endpoints is similar to the JWT flow for xApps, except the JWT is obtained through the OAuth2 flow instead of inside the xApp.

{% hint style="info" %}
All JWTs the obtained by a successful user sign in are valid for **one day (24h)**
{% endhint %}

## Sample code

...

## User properties (userinfo-endpoint)

...

## OAuth2 & OpenID Connect endpoints

...

| Endpoint type                         | Path (URL linked)                                                                                            |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Authorization                         | oauth2.xumm.app/[auth](https://oauth2.xumm.app/auth)                                                         |
| Token                                 | oauth2.xumm.app/[token](https://oauth2.xumm.app/token)                                                       |
| Userinfo                              | oauth2.xumm.app/[userinfo](https://oauth2.xumm.app/userinfo)                                                 |
| JWKS                                  | oauth2.xumm.app/[certs](https://oauth2.xumm.app/certs)                                                       |
| OpenID Connect Metadata               | oauth2.xumm.app/[.well-known/openid-configuration](https://oauth2.xumm.app/.well-known/openid-configuration) |
| _All other JWT compatible Xumm API's_ | See our API docs: [reference/oauth2-jwt](https://xumm.readme.io/reference/oauth2-jwt)                        |
