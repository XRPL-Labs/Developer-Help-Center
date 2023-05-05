---
description: >-
  Developers can use the Xumm SDK to easily integrate with the Xumm platform.
  This allows for easy & secure end user interaction. With your application &
  the XRP Ledger.
---

# Xumm SDK (Intro)

## JavaScript/TypeScript

### NPM

The Xumm Javascript/TypeScript SDK can be found on **npm**:

{% embed url="https://www.npmjs.com/package/xumm" %}

### CDN

The latest version of the Xumm SDK is always available at:

```
https://xumm.app/assets/cdn/xumm.min.js
```

{% hint style="info" %}
Please note the CDN URL is heavily cached (edge and headers, so client side). If you are expecting a new version of the SDK to load, consider cleaning local cache and adding a random (e.g. your build hash) as a URL Query param to the URL to force URL uniqueness.
{% endhint %}

### Code samples

See [examples-user-stories](examples-user-stories/ "mention")

### Warning (legacy packages)

{% hint style="warning" %}
Previously there were three different packages:

* `xumm-sdk`for backend interaction
* `xumm-xapp-sdk` for xApp frontend interaction
* `xumm-oauth2-pkce` for browser / "Web3" interaction

**All three packages above have been replaced by the** [**`xumm`**](https://www.npmjs.com/package/xumm) **package, which allows for easier (unified) interaction with the three aforementioned topics.**
{% endhint %}
