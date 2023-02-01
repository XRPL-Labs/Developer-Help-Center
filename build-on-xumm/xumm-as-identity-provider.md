---
description: >-
  The Xumm platform can act as the OAuth2 provider. The Xumm platform supports
  the OAuth2 / OpenID Connect flow. Authenticate and identify end users using
  their self custodial XRPL accounts.
---

# Xumm as identity provider

## Client side web apps

The Xumm OAuth2 / OpenID Connect provider supports the **authorization code** flow and the **implicit flow**. The **PKCE flow** (which is the new & more secure industry standard and replaces the Implicit flow) is also available.&#x20;

{% embed url="https://oauth2-pkce-demo.xumm.dev/" %}
Xumm OAuth2 / PKCE examples (client side only)
{% endembed %}

## Identity provider (OAuth2, OpenID Connect)

You can use self custodial XRP Ledger accounts to identify your users, and allow for convenient sign in. The Xumm OAuth2 platform is OpenID Connect compatible, and can thus be used with most OAuth2 / OpenID Connect consumers.

{% hint style="info" %}
As per OAuth2 standards, our **`/userinfo`** endpoint return the **`sub`** field, containing the r-address of the user that signed in. This value can be used to identify the unique user.
{% endhint %}

## Implementation

Read more about building using Xumm as identity provider:

{% content-ref url="../environments/identity-oauth2-openid/" %}
[identity-oauth2-openid](../environments/identity-oauth2-openid/)
{% endcontent-ref %}
