---
description: >-
  Once a payment has been sent and the payload resolved on Xumm, some checks are
  performed to ensure secure payment verification. This document walks you
  through verifying a payment transaction on Xumm.
---

# 🚨 Secure Payment Verification

### **Payload Completion and Verification**

After a payload completes its lifecycle, which includes creation, user interaction, transaction signing, and transaction submission to the XRP Ledger by Xumm, your application will receive (if configured) a Webhook callback.&#x20;

This callback should trigger your application to fetch the payload results. It is **highly advisable** to fetch the payload results again on your "thank you" or "return" page in case you did not persist the payload results after receiving a Webhook.

### **Verifying Payment Transactions**

Here are the steps to **verify that you have indeed received a payment**:

1. **Check Payload Output**: Verify if the Payload output contains `meta.resolved`. This value should be `true`. Otherwise, the payload is still pending or has been abandoned by the user. Also, check if the Payload output contains `meta.signed`. This value should be `true`, indicating that the user signed the transaction.
2. **Check Response Dispatched Node Type**: Verify the `response.dispatched_nodetype` value. If you are expecting a **real** payment, this value should contain `MAINNET`. If it doesn't**,** you ⚠️ might be accepting a TESTNET payment.
3. **Check Transaction ID**: The `response.txid` value is the on-ledger transaction hash. You must **verify** this transaction on the ledger. Note that it may take around 4 seconds for a ledger to close and slightly longer for the ledger and transaction info to propagate. You may want to repeat async/delay fetching this info if you don't get a result at first or if your result contains a `validated`: `false` value.
4. [⚠️](https://emojipedia.org/warning/) **Check Delivered Amount**: After fetching the transaction details, check the `meta.delivered_amount` value to see if the amount of XRP (in drops, one million drops = one XRP) equals the expected amount to be paid. This is a crucial step in the verification process.

### **Fetching Transaction Details**

You can fetch transaction details using the XRPL Transaction Data fetcher  [![npm version](https://badge.fury.io/js/xrpl-txdata.svg)](https://www.npmjs.com/xrpl-txdata) [![GitHub Actions NodeJS status](https://github.com/XRPL-Labs/XrplTxData/workflows/NodeJS/badge.svg?branch=main)](https://github.com/XRPL-Labs/XrplTxData/actions) [![CDNJS Browserified](https://img.shields.io/badge/cdnjs-browserified-blue)](https://cdn.jsdelivr.net/gh/XRPL-Labs/XrplTxData@main/dist/browser.js) [![CDNJS Browserified Minified](https://img.shields.io/badge/cdnjs-minified-orange)](https://cdn.jsdelivr.net/gh/XRPL-Labs/XrplTxData@main/dist/browser.min.js) or the JSON RPC (HTTP POST) method at [https://xrplcluster.com](https://xrplcluster.com/).

### Utilizing (flow+code) the `xrpl-txdata` Package (JS/TS) for Transaction Verification

After sending a Sign Request ([payload](https://docs.xumm.dev/concepts/payloads-sign-requests)) to Xumm, you receive a response with the signed **transaction hash** ([Webhook](https://docs.xumm.dev/concepts/payloads-sign-requests/status-updates/webhooks): `payloadResponse.txid`, [WebSocket](https://docs.xumm.dev/concepts/payloads-sign-requests/status-updates/websocket): `txid`).

You're in luck if you immediately check this transaction hash on the XRP Ledger, and it's already in a validated ledger. However, if the transaction hasn't been included in a closed ledger, you might encounter a "Not Found" error, while if you had checked a few seconds later, you'd have found the transaction.

To streamline this process, use the `xrpl-txdata` NPM package (JS/TS). This package simplifies:

1. Establishing a redundant (multi-node, failover) and reliable (auto-timeout, auto-retry) connection to the XRP Ledger
2. Fetching a transaction by hash
3. Optionally, monitoring the XRP Ledger (all closed ledgers, all the transactions in those ledgers) and waiting for a specified time (seconds).

Once your transaction is found, the package returns the transaction outcome and validated balance changes.&#x20;

**Here's how to use it in JavaScript:**

```javascript
const {TxData} = require('xrpl-txdata')

const TxHash = '8F3CE0481EF31A1BE44AD7D744D286B0F440780CD0056951948F93A803D47F8B'

const VerifyTx = new TxData([
  'wss://xrplcluster.com',
  'wss://xrpl.link',
  // Or:
  // 'wss://testnet.xrpl-labs.com'
], {
  OverallTimeoutMs: 6000,
  EndpointTimeoutMs: 1500,
  // If using testnet, see above:
  // AllowNoFullHistory: true
})

// Specify the transaction hash to verify and the # of seconds
// to wait & monitor the XRPL if not found initially.
VerifyTx.getOne(TxHash, 20)
  .then(tx => {
    console.log(`Got the TX, details:`, tx)
  })
```

**Good Practice: Cross-verify with the XRPL**

It is always a good practice to cross-verify with the XRPL for absolute certainty. Using the `tx` method, you can fetch transaction details directly from the XRPL ledger.&#x20;

More information on how to do this can be found in the [XRPL Transaction Documentation](https://xrpl.org/tx.html#tx).
