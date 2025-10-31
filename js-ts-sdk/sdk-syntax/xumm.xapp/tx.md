---
description: Open the Transaction Details panel
---

# tx({ … })

## Parameters

```javascript
{
  account: '...',
  tx: 'HASH...',
  network?: 'MAINNET|TESTNET|XAHAU|...',
}
```

## Syntax

```javascript
xumm.xapp.tx({
  account: 'rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ',
  tx: '250DC3E83946EFE965DE36B3F9AE8608CD7ED793657BDEC5B794B665B2DCBC0E',
  network: 'MAINNET',
})
```

## Requirement(s)

* The given `account` must be imported in Xumm
* Xumm must be on the network the transaction is present on
