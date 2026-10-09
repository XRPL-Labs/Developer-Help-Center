---
description: >-
  Build your own web app to live in-app, inside Xaman for all Xaman users. Build
  an xApp. Use your favourite tools & frameworks for the client side code (HTML,
  CSS, JS, etc.
---

# 📱 xApps ("dApps")

xApps are web apps. They are offered to users as integrated apps, opened in Xaman for a great user experience. They add value (tools, apps, wizards, ...) for end users. They receive context information when opened, and can interact with some of the native Xaman features & users through Sign Requests.

{% hint style="info" %}
Please read carefully: [requirements.md](requirements.md "mention")
{% endhint %}

## Permissions

xApps have extra special permissions, allowing the xApp (web app) to interact with some of the native Xaman features:

* They receive context (user account selected in Xaman when opened, Xaman theme, input params, account type (eg. Tangem / ...)
* They can trigger overlay Sign Requests and receive callback info
* They can trigger the QR scanner and receive scanned QR data

## Opening xApps

xApps can be opened (triggered) in lots of ways:

* In the Xaman shortlist (we feature some apps, they get replaced by frequently used apps by the user)
* From the xApp directory
* By opening a deeplink (browser / from within another app)
* By scanning a QR code

{% hint style="info" %}
To prevent showing a double loader (first the Xaman xApp loader, then your xApp's loader while hydrating / booting) you can enable the "**Xaman Loader Screen**" option in the Xaman Developer Console (xApp tab).\
See [ready.md](../../js-ts-sdk/sdk-syntax/xumm.xapp/ready.md "mention")
{% endhint %}

### Advanced ways to open xApps

* By attaching an xApp memo to an XRPL TX (so the Event list will show there's an xApp attached to the TX)
* Using push notifications
* From the Event list, as an xApp session pushed to a Xaman user

## xApp example use cases

* Trading interface (offloads signing to Xaman)
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
      var xaman = new Xaman('your-api-key')
      
      xaman.on("ready", () => console.log("Ready (e.g. hide loading state of xApp)"))
  
      // Account can't change (like Web3 logout/login) so we can rely on the promise
      xaman.user.account.then(account => {
        document.getElementById('accountaddress').innerText = account
      })
    </script>
  </body>
</html>
```
