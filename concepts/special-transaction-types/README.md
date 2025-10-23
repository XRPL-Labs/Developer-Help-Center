---
description: >-
  In Xaman, you can use all XRPL transaction types when sending a JSON
  transaction payload. However, some special transaction types are unique to
  Xaman, or require some extra info to use them.
---

# Special Transaction Types

{% content-ref url="signin.md" %}
[signin.md](signin.md)
{% endcontent-ref %}

{% content-ref url="batch-multiple-inner-signers.md" %}
[batch-multiple-inner-signers.md](batch-multiple-inner-signers.md)
{% endcontent-ref %}

{% content-ref url="paymentchannelauthorize.md" %}
[paymentchannelauthorize.md](paymentchannelauthorize.md)
{% endcontent-ref %}

\


* `PaymentChannelAuthorize` \
  Is normally a 'Command' or locally signed object. Implemented in Xumm as a TransactionType (which it actually isn't, also: the resulting signed blob **can never be submitted to an XRPL node as is**). For more information, see: [https://xrpl.org/use-payment-channels.html](https://xrpl.org/use-payment-channels.html)\
  **Sample PayChan transactions (gist):**\
  [https://gist.github.com/WietseWind/c7b6addfd9b8cb465894209cc9073c47](https://gist.github.com/WietseWind/c7b6addfd9b8cb465894209cc9073c47)

**Note**: The `SignIn` transaction type is particularly useful when you want to authenticate a user without performing any transaction on the XRPL. The `PaymentChannelAuthorize` transaction type, on the other hand, is useful when you want to authorize a payment channel without submitting a transaction to the XRPL.
