---
description: >-
  Xumm supports a wide range of transaction types to cater to various use cases
  on the XRPL. Here's what you need to know:
---

# Transaction types

*   **Standard Transaction Types**: Xumm accepts all mainnet XRPL transaction types.

    * Exception: Transaction types for non-voted in amendments may be unavailable
    * Payment Channel signature types (non-transaction, receipt) are not yet supported (to be added in Xumm 2.5.0)


* **Pseudo-Transaction Types**: One pseudo-transaction type: `SignIn` - [user-identification-payloads.md](../../environments/backend-sdk-api/user-identification-payloads.md "mention")
* **Limited Transaction Types:**: Some transaction types, such as setting a Regular Key or setting a Signer List (multisign), require special permission for user security reasons:
  * Setting a Regular Key
  * Setting a Signer List (multisign)
