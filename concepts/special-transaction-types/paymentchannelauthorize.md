---
description: >-
  To authorize a Payment Channel, an off ledger "receipt" must be signed. This
  is implemented in Xaman through a 'Pseudo Transaction' with TransactionType
  `PaymentChannelAuthorize`.
icon: bridge-suspension
---

# PaymentChannelAuthorize

`PaymentChannelAuthorize` is normally a 'Command' or locally signed object. Implemented in Xumm as a TransactionType (which it actually isn't, also: the resulting signed blob **can never be submitted to an XRPL node as is**). For more information, see: [https://xrpl.org/use-payment-channels.html](https://xrpl.org/use-payment-channels.html)

## **Sample PayChan transactions (gist):**

[**https://gist.github.com/WietseWind/c7b6addfd9b8cb465894209cc9073c47**\
](https://gist.github.com/WietseWind/c7b6addfd9b8cb465894209cc9073c47)

{% hint style="success" %}
Note: the **PaymentChannelAuthorize** transaction type is useful when you want to authorize a payment channel without submitting a transaction to the XRPL.
{% endhint %}
