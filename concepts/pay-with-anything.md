---
description: >-
  Xaman allows you to easily craft a payload (Sign Request) that will always
  deliver the currency and amount you want to receive, while allowing the Xaman
  user to pay with anything (any asset they have)
---

# "Pay With Anything"

## The Payload

To request delivery of 5 RLUSD:

```mjs
{
  options: {
    force_network: 'MAINNET',
    pathfinding: true
  },
  custom_meta: {
    instruction: 'Pay for this and that...'
  },
  txjson: {
    TransactionType: 'Payment',
    Destination: 'r...YourAddress...',
    Amount: {
      currency: '524C555344000000000000000000000000000000',
      issuer: 'rMxCKbEDwqr76QuheSUMdEGf4B9xJ8m5De',
      value: '15'
    }
  }
}
```

It's as simple as that. Xaman sees Amount, Xaman sees pathfinding in the option and done!

You will always get what you asked for, user can pay with anything. `delivered_amount` is always your preferred currency from `Amount`.

## The Sign Request (user facing)

When a payload like above is opened by the user, they will have to wait a few seconds for the XRP Ledger to finish a Pathfinding request, to see which assets the user posesses that can satisfy delivering the requested amount (with in-line, in-transaction, atomic conversion of the asset the user sends to the asset you want to receive).

| First few seconds                                                        | After paths are found                                                    |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| <img src="../.gitbook/assets/image (2).png" alt="" data-size="original"> | <img src="../.gitbook/assets/image (3).png" alt="" data-size="original"> |
