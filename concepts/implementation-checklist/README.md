---
description: >-
  This article presents a concise implementation checklist for developers using
  Xumm. By following these steps, you can ensure a smooth and secure integration
  whilst optimizing the user experience.
---

# Implementation checklist

* [ ] **Verify transactions on ledger:** [verify-transactions.md](../payloads-sign-requests/verify-transactions.md "mention")

1. **Fetch Payload Results:** Trigger your application to fetch payload results after receiving a Webhook callback.
2. **Inspect Payload Output:** Confirm `meta.resolved` and `meta.signed` are both true in the payload output.
3. **Identify Dispatched Node Type:** Ensure `response.dispatched_nodetype` is "MAINNET" for real payments.
4. **Validate Transaction ID:** Validate the `response.txid` value on the ledger.
5. **Examine Delivered Amount:** Confirm the `meta.delivered_amount` equals the expected payment amount.
6. **Use xrpl-txdata Package:** Establish a connection to the XRP Ledger, fetch the transaction by hash, and cross-verify transaction details with the XRPL ledger.

* [ ] **Consider the end user network:** [networks.md](../payloads-sign-requests/networks.md "mention")

1. **Network Independence:** Use the Xumm API/SDK, which operates independently of the network, to allow users the freedom of network choice.
2. **Network Information:** Ensure the results of a signed payload include the network the user was on during the signing.
3. **Forced Network Identifier:** Check for the expected result in the Payload results or specify a particular network using a forced network identifier in a payload.
4. **OTT Data:** Utilize xApp OTT data, including network information, to better manage transactions.
5. When linking to Transaction Details using a Transaction Explorer, consider using our helper tooling: [tx-explorer-s.md](../payloads-sign-requests/tx-explorer-s.md "mention")

* [ ] **Verify Webhook signatures:** [signature-verification.md](../payloads-sign-requests/status-updates/webhooks/signature-verification.md "mention")

1. **Secure Your Webhooks:** Implement appropriate security measures.
2. **Verify Payloads:** Authenticate received payloads.
3. **Error Handling:** Develop robust error management mechanisms.

* [ ] **Protecting your application from the "partial payments exploit"** is crucial when implementing payment functionalities. Instead of relying on the `Amount` field, which merely indicates the transaction instruction, you should base your logic on the `delivered_amount` field in the transaction metadata. The `Amount` field is the **instruction**, and the **delivered\_amount** metadata field is the result. For more detailed information, please refer to the [XRPL.org documentation](https://xrpl.org/partial-payments.html#the-delivered\_amount-field).\

* [ ] **xApps**: [requirements.md](../../environments/xapps-dapps/requirements.md "mention")

1. **xApp Creation & Audit:** Anyone can create sandbox xApps, but public release requires an audit by XRPL Labs for user safety, compliance, and value addition.
2. **User Experience:** xApps must be self-explanatory, prevent dangerous mistakes, and provide a unique experience tailored to Xumm users.
3. **Technical & Styling Standards:** xApps must meet Xumm's technical guidelines and respect or have unique styling.
4. **Transparency & Support:** Developers cannot be anonymous and must provide a clear support workflow, terms & conditions, and a privacy statement.
