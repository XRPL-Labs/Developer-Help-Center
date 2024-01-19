---
description: >-
  To easily link to transaction explorers, you can link to the Xumm explorer
  launchpad and allow users to pick their preferred explorer.
---

# Tx Explorer(s)

Don't keep a list of explorer links youself: you can easily rely on our explorer launchpad URL.&#x20;

### When using TX Hash

```
https://xumm.app/explorer/{network}/{txhash}
```

The `network` param can be `mainnet`, `xahau` and any other key from the `rails` endpoint [https://xumm.app/api/v1/platform/rails](https://xumm.app/api/v1/platform/rails) - also available in our SDK: [getrails.md](../../js-ts-sdk/sdk-syntax/xumm.helpers/getrails.md "mention")

### When using CTID&#x20;

CTID is a more efficient way to link to transactions, as they contain the ledger index, transaction index in that ledger and the NetworkID.

More info: [https://xrpl.org/ctid.html](https://xrpl.org/ctid.html)

```
https://xumm.app/explorer/{ctid}
```

