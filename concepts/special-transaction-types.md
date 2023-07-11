---
description: >-
  In Xumm, you can use all XRPL transaction types when sending a JSON
  transaction payload. However, some special transaction types are unique to
  Xumm.
---

# Special Transaction Types

**Pseudo Transactions:**

*   `SignIn`\
    **Xumm specific, signature only, can never be submitted.** When sending a JSON transaction payload, you can use all XRPL transaction types, including a Xumm-specific "pseudo transaction type": `SignIn`.\


    The payload for a SignIn transaction can look like this:

    ```json
    {
      "txjson": {
        "TransactionType": "SignIn"
      }
    }
    ```

    \
    After the user signs your SignIn request, the server-to-server call (to your configured Webhook location) will receive the signed transaction containing the signed transaction HEX blob.

    You can verify the signature using the `verify-xrpl-signature` package:\
    [https://github.com/XRPL-Labs/verify-xrpl-signature](https://github.com/XRPL-Labs/verify-xrpl-signature)\

* `PaymentChannelAuthorize` \
  Is normally a 'Command' or locally signed object. Implemented in Xumm as a TransactionType (which it actually isn't, also: the resulting signed blob **can never be submitted to an XRPL node as is**). For more information, see: [https://xrpl.org/use-payment-channels.html](https://xrpl.org/use-payment-channels.html)

**Note**: The `SignIn` transaction type is particularly useful when you want to authenticate a user without performing any transaction on the XRPL. The `PaymentChannelAuthorize` transaction type, on the other hand, is useful when you want to authorize a payment channel without submitting a transaction to the XRPL.
