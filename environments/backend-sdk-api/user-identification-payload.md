---
description: >-
  When building your own backend integration, you can request a user to sign a
  Sign Request with a "SignIn" transaction type. This is a pseudo transaction
  type allowing a user to confirm their r-address
---

# User identification (payload)

{% hint style="info" %}
A SignIn transaction will **never** be submitted to the XRP ledger, as it is an invalid transaction type (XUMM specific pseudo transaction type).
{% endhint %}

A sign `SignIn` sign request can be as simple as this:

```json
{
  "txjson": {
    "TransactionType": "SignIn"
  }
}
```

All Xumm payload options are valid for a `SignIn` transaction.

\
After the user signs your SignIn request, the server to server call (to your configured Webhook location) will receive the signed transaction containing the signed transaction HEX blob.

## Response

When the user signs the Sign Request, you will get a signed transaction (that has never been submitted to the XRP Ledger).&#x20;

You can now get the account address and some basic public account information from the payload details, and assign this information to your own local dataset, like a session.

### Verify the signature

If you want to you can run your own signature verification on the signed `SignIn` pseudo transaction our platform returns to you. Of course the Xumm platform also verified the signature for you. Would you like to check yourself as well, we have created this package

{% embed url="https://www.npmjs.com/package/verify-xrpl-signature" %}

### &#x20;
