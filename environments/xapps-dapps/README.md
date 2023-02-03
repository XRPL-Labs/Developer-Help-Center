---
description: >-
  Build your own web app to live in-app, inside Xumm for all Xumm users. Build
  an xApp. Use your favourite tools & frameworks for the client side code (HTML,
  CSS, JS, etc.
---

# xApps ("dApps")

xApps are web apps. They are offered to users as integrated apps, opened in Xumm for a great user experience. They add value (tools, apps, wizards, ...) for end users. They receive context information when opened, and can interact with some of the native Xumm features & users through Sign Requests.

## Permissions

xApps have extra special permissions, allowing the xApp (web app) to interact with some of the native Xumm features:

* They receive context (user account selected in Xumm when opened, Xumm theme, input params, account type (eg. Tangem / ...)
* They can trigger overlay Sign Requests and receive callback info
* They can trigger the QR scanner and receive scanned QR data

## Open xApps

xApps can be opened (triggered) in lots of ways:

* In the Xumm shortlist (we feature some apps, they get replaced by frequently used apps by the user)
* From the xApp directory
* By opening a deeplink (browser / from within another app)
* By scanning a QR code

### Advanced ways to open xApps

* By attaching an xApp memo to an XRPL TX (so the Event list will show there's an xApp attached to the TX)
* Using push notifications
* From the Event list, as an xApp session pushed to a Xumm user

## Examples

* Trading interface (offloads signing to Xumm)
* Admission ticket checking
* NFT marketplaces / viewers
* Issuing tokens, checking tokens
* Tools: setting up accounts, crafting advanced transactions, escrows, etc.
* Exchange deposit / withdraw integrations
