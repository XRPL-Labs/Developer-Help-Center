# Transaction types

* All (mainnet) XRPL transaction types are accepted
  * Exception: Transaction types for non-voted in amendments may be unavailable
  * Payment Channel signature types (non-transaction, receipt) are not yet supported (to be added in Xumm 2.5.0)
* One pseudo-transaction type: `SignIn` - [user-identification-payloads.md](../../environments/backend-sdk-api/user-identification-payloads.md "mention")
* Two transactions types limited (require special permission, for user security reasons):
  * Setting a Regular Key
  * Setting a Signer List (multisign)
