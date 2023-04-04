---
description: Xumm allows developers and app users to "meet up".
---

# Getting started

While app users can simply use the Xumm application interact with the XRP Ledger with their accounts, balances and transactions, the true power of Xumm is unleashed through the platform available for developers.

This way users can interact with third party tools & platforms in the most secure and convenient way, while developers don't have to worry about wallet & key management.

## Concept

XRP Ledger transactions are traditionally user initiated: users open their wallet, enter the destination, amount, etc. and then you submit a transaction. This is referred to as a _Push Transaction_.

In retail / e-commerce & third party interaction scenarios, the ideal flow is inverted: a _Pull Transaction_. The third party environment wants the user to sign a specific transaction, and a transaction to sign is offered to the user.

This is where the Xumm platform comes in. An XRP Ledger _transaction template_ can be delivered to the end user through the Xumm platform. This is called a Sign Request.

## Interaction

The most convenient way to interact with the Xumm platform is through the JavaScript/TypeScript SDK: [Broken link](broken-reference "mention"). There are also some other SDKs available for **Backend** use in other languages:

| Language                    | Maintenance     | Package                                                                                                                          |
| --------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Typescript / Javascript** | **XRPL Labs** ⭐ | [![npm version](https://badge.fury.io/js/xumm.svg)](https://www.npmjs.com/xumm) / [CDN](https://xumm.app/assets/cdn/xumm.min.js) |
| Python                      | Community       | [![python version](https://badge.fury.io/py/xumm-sdk-py.svg)](https://pypi.org/project/xumm-sdk-py/)                             |
| C# (.NET)                   | Community       | [![NuGet version](https://badge.fury.io/nu/XUMM.NET.SDK.svg)](https://badge.fury.io/nu/XUMM.NET.SDK)                             |
| PHP                         | Community       | [![Packagist PHP version](https://badgen.net/badge/PHP%20Package/8.1/green)](https://packagist.org/packages/xrpl/xumm-sdk-php)   |

The Xumm platform allows for easy integration in your application & workflow. Make sure to check the documentation for your environment:

<table data-card-size="large" data-column-title-hidden data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../environments/browser-web3/">browser-web3</a></td><td></td><td></td><td></td></tr><tr><td><a href="../environments/xapps-dapps/">xapps-dapps</a></td><td></td><td></td><td></td></tr><tr><td><a href="../environments/backend-sdk-api.md">backend-sdk-api.md</a></td><td></td><td></td><td></td></tr><tr><td><a href="../environments/native-apps.md">native-apps.md</a></td><td></td><td></td><td></td></tr></tbody></table>
