# Implementation checklist

* [ ] Verifying transactions on ledger? [verify-transactions.md](payloads-sign-requests/verify-transactions.md "mention")
* [ ] Taking the network of the end user into account? [networks.md](payloads-sign-requests/networks.md "mention")
* [ ] Webhooks: [signature-verification.md](payloads-sign-requests/status-updates/webhooks/signature-verification.md "mention")
* [ ] If you are relying on payments: make sure to safeguard your application logic against the "partial payments exploit". TL;DR: rely on the transaction meta `delivered_amount` field instead of the `Amount` field: the `Amount` field is the **instruction**, the **delivered\_amount** metadata field is the result. See the [XRPL.org documentation](https://xrpl.org/partial-payments.html#the-delivered\_amount-field).
