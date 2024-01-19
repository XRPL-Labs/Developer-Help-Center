---
description: >-
  The XRP Ledger Protocol has several protocol-related things to check in your
  app/implementation to make the experience for end users better. Please take
  these things into account:
---

# Protocol specific checks

* [ ] Partial Payments: if you are processing received payments: **make sure to check the `delivered_amount` (meta) field** for the transaction outcome, and not the `Amount` field. Amount is the instruction, Delivered Amount is the actual delivered amount, which may be lower.\
  \
  See: [https://xrpl.org/partial-payments.html](https://xrpl.org/partial-payments.html)
*   [ ] When determining if users are able to send funds, make sure to take the Account and Owner reserve into account. See: [https://xrpl.org/reserves.html](https://xrpl.org/reserves.html)\
    You can obtain them with a `server_info` and `account_info` call on the chain (tip: use [https://www.npmjs.com/package/xrpl-client](https://www.npmjs.com/package/xrpl-client) to interact with the network). Then calculate like this:\


    ```ini
    ownerwnerCount = accountInfo.account_data.OwnerCount
    reserveBase = serverInfo.info.validated_ledger.reserve_base_native || serverInfo.info.validated_ledger.reserve_base_xrp
    reserveInc = serverInfo.info.validated_ledger.reserve_inc_native || serverInfo.info.validated_ledger.reserve_inc_xrp
    ```
* [ ] Use **WebSockets** over HTTP RPC (JSON POST) if you want realtime status updates from the ledger using the `subscribe` method. You can subsribe to ledger closes, transaction stream and account activity: [https://xrpl.org/subscribe.html](https://xrpl.org/subscribe.html)
