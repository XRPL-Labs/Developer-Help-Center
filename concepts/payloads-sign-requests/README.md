---
description: >-
  Xumm Payloads: creating, delivering, and utilizing incomplete XRP Ledger
  transactions as a Sign Request to end users.
---

# Payloads (sign requests)

The difference between XRP Ledger Transaction JSON and a Xumm Payload is that the XRP Ledger JSON needs to be complete and signed locally, while a Xumm Payload can contain an incomplete transaction.

The incomplete transaction, referred to as a Transaction Template, can be delivered to Xumm users so an end user can view the Payload.

Xumm will then add the missing fields like the signer account, network Fee, Account Sequence, based on the context the user provides.

Xumm Payloads use the exact same syntax as the XRP Ledger JSON transaction format.

{% hint style="info" %}
To easily test a payload, you can enter the Transaction JSON template on this page and try to create a payload:\
[**https://xumm.dev/signing-tool**](https://xumm.dev/signing-tool?payload=eyJUcmFuc2FjdGlvblR5cGUiOiJQYXltZW50IiwiQWNjb3VudCI6InJURVNUd1BVTjlSYm9DQmdFWHFLYnBrVHFEQ2V3TUhLOSIsIkRlc3RpbmF0aW9uIjoiclNUQVlLeEYySzc3WkxaOEdvQXdUcVBHYXBoQXFNeVhWIiwiQW1vdW50IjoiMTYxMTYiLCJQYXRocyI6W3siY3VycmVuY3kiOiJTVFgiLCJpc3N1ZXIiOiJyU1RBWUt4RjJLNzdaTFo4R29Bd1RxUEdhcGhBcU15WFYifV0sIkZlZSI6IjE1In0=)
{% endhint %}

Your application crafts the XRPL transaction template. The difference between a regular XRPL JSON transaction and a Xumm transaction template is that you can leave out some fields (or leave them blank) as the Xumm app on the device of the end user will fill them automatically.

Your application backend will send the transaction template to the Xumm API / SDK. Your application will receive a unique Payload ID that contains your Sign Request.

### Typical fields Xumm provides:

* **Fee** will be automatically filled with the appropriate network fee, but when set in the Payload, Xumm will respect your provided fee.
* **Sequence** will be automatically filled with the Account sequence of the account interacting with your payload.
* **Account** will be automatically filled with the account interacting with your payload.
