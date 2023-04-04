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

## Opening xApps

xApps can be opened (triggered) in lots of ways:

* In the Xumm shortlist (we feature some apps, they get replaced by frequently used apps by the user)
* From the xApp directory
* By opening a deeplink (browser / from within another app)
* By scanning a QR code

{% hint style="info" %}
To prevent showing a double loader (first the Xumm xApp loader, then your xApp's loader while hydrating / booting) you can enable the "**Xumm Loader Screen**" option in the Xumm Developer Console (xApp tab). The xApp will then show the Xumm native loader, until your application calls the `ready()` method on the Xumm SDK.
{% endhint %}

### Advanced ways to open xApps

* By attaching an xApp memo to an XRPL TX (so the Event list will show there's an xApp attached to the TX)
* Using push notifications
* From the Event list, as an xApp session pushed to a Xumm user

## xApp example use cases

* Trading interface (offloads signing to Xumm)
* Admission ticket checking
* NFT marketplaces / viewers
* Issuing tokens, checking tokens
* Tools: setting up accounts, crafting advanced transactions, escrows, etc.
* Exchange deposit / withdraw integrations

## Sample code

```html
<html lang="en">
  <body>
    <h1 id="accountaddress">...</h1>
        
    <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
    <script>
      var xumm = new Xumm('your-api-key')
      
      xumm.on("ready", () => console.log("Ready (e.g. hide loading state of xApp)"))
  
      // Account can't change (like Web3 logout/login) so we can rely on the promise
      xumm.user.account.then(account => {
        document.getElementById('accountaddress').innerText = account
      })
    </script>
  </body>
</html>
```
