---
description: >-
  You focus on building your cool app. We make sure your app & Xumm users can
  interact. Safely & smoothly.
---

# Build on Xumm

**Welcome to the Xumm Developer Docs!**\
\
**Xumm is a powerful platform designed to make your interaction with the XRP Ledger (XRPL) seamless. Whether you are an experienced developer or just getting started, Xumm offers a range of features, including xApps, payloads, transaction signing, and much more.**\
\
**This documentation will guide you through the essentials to get you up and running in no time.**

While app users can simply use the Xumm app to manage their XRP ledger accounts, balances and transactions, the true power of Xumm can be experienced through the Xumm SDK, using our platform made available for developers.



{% hint style="success" %}
Want to dive straight in? You're one click away from the [examples-user-stories](js-ts-sdk/examples-user-stories/ "mention")
{% endhint %}

## Ways to interact

The Xumm SDK can be used to interact with Xumm users. An example can be a "sign request", where the user is asked to sign a transaction, identification (sign in) or a user interface presented in Xumm (xApp).

{% hint style="info" %}
What are you going to build? Read more about specific user & developer flows:
{% endhint %}

<table data-column-title-hidden data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Client side web apps "Web3"</strong></td><td><a href="environments/browser-web3/">browser-web3</a></td><td><a href=".gitbook/assets/browsers.png">browsers.png</a></td></tr><tr><td><strong>xApps: your web app in Xumm</strong></td><td><a href="environments/xapps-dapps/">xapps-dapps</a></td><td><a href=".gitbook/assets/xapps.png">xapps.png</a></td></tr><tr><td><strong>Backend integrations</strong></td><td><a href="environments/backend-sdk-api.md">backend-sdk-api.md</a></td><td><a href=".gitbook/assets/nodejs.png">nodejs.png</a></td></tr><tr><td><strong>Xumm as Identity Provider</strong></td><td><a href="environments/identity-oauth2-openid/">identity-oauth2-openid</a></td><td><a href=".gitbook/assets/openid.png">openid.png</a></td></tr></tbody></table>

## Packages

The Xumm SDK offers a ready to use Javascript & Typescript SDK for all frontend and backend projects. With only minor differences depending on the environment you are using the SDK in, the SDK is the most convenient way to interact with Xumm users & the Xumm ecosystem.

If you are not working in a [Javascript/Typescript](https://www.npmjs.com/package/xumm) environment and prefer to build your own backend implementation, you can use our [API (endpoint) documentation](https://xumm.readme.io/v1.0/reference/post-payload) or use one of our SDKs for [Python (PyPI)](https://pypi.org/project/xumm-sdk-py/), [PHP (Packagist)](https://packagist.org/packages/xrpl/xumm-sdk-php) or [C# (NuGet)](https://www.nuget.org/packages/XUMM.NET.SDK)

| Language                    | Maintenance     | Package                                                                                                                          |
| --------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Typescript / Javascript** | **XRPL Labs** ⭐ | [![npm version](https://badge.fury.io/js/xumm.svg)](https://www.npmjs.com/xumm) / [CDN](https://xumm.app/assets/cdn/xumm.min.js) |
| Python                      | Community       | [![python version](https://badge.fury.io/py/xumm-sdk-py.svg)](https://pypi.org/project/xumm-sdk-py/)                             |
| C# (.NET)                   | Community       | [![NuGet version](https://badge.fury.io/nu/XUMM.NET.SDK.svg)](https://badge.fury.io/nu/XUMM.NET.SDK)                             |
| PHP                         | Community       | [![Packagist PHP version](https://badgen.net/badge/PHP%20Package/8.1/green)](https://packagist.org/packages/xrpl/xumm-sdk-php)   |
