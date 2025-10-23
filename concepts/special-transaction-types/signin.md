---
description: >-
  The `SignIn` payload is a "Pseudo transaction type": an off ledger transaction
  specific to Xaman, which can be used to identify a user and obtain a token to
  push sign requests to the end user.
icon: signature-lock
---

# SignIn

{% hint style="success" %}
Note that the `SignIn` transaction type is already embedded in the Xaman SDK and OAuth flows. You only need the `SignIn` transaction type if you are manually building your own integrations (e.g. API integrations:[backend-sdk-api.md](../../environments/backend-sdk-api.md "mention"))
{% endhint %}

**The SignIn transaction type is Xaman specific, signature only, can never be submitted.** When sending a JSON transaction payload, you can use all XRPL transaction types, including a Xumm-specific "pseudo transaction type": `SignIn`.

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
[https://github.com/XRPL-Labs/verify-xrpl-signature](https://github.com/XRPL-Labs/verify-xrpl-signature)

**Note**: The `SignIn` transaction type is particularly useful when you want to authenticate a user without performing any transaction on the XRPL.
