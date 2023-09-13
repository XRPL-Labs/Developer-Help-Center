---
description: >-
  Fetch an XRPL transaction & metadata. Please don't use this method unless
  absolutely necessary: please set up your own connection to an XRPL node to
  fetch this information.
---

# getTransaction( … )

The `getTransaction` method allows you to get the transaction outcome (mainnet) live from the XRP ledger, as fetched for you by the XUMM backend.

**Note**: it's best to retrieve these results **yourself** instead of relying on the XUMM platform to get live XRPL transaction information! You can use the [**xrpl-txdata**](https://www.npmjs.com/package/xrpl-txdata) package to do this:\
[![npm version](https://badge.fury.io/js/xrpl-txdata.svg)](https://www.npmjs.com/xrpl-txdata)

```typescript
const txInfo = await Sdk.getTransaction(txHash);
```

Returns: [`<XrplTransaction>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Meta/XrplTransaction.ts)
