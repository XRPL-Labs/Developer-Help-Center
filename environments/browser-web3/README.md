---
description: >-
  Building a web app? Running as a client side SPA (single page webapp) or
  server side rendered? React Native / VueJS / VanillaJS / etc.: you can
  integrate with the Xumm ecosystem using our SDK.
---

# Browser ("Web3")

The Xumm SDK can run fully client side: either as part of your compiled web app or using plain HTML and Javascript using our ready to use [browserified](https://xumm.app/assets/cdn/xumm.min.js) version.

Using the Xumm SDK, you can easily add "Sign in with Xumm" capabilities to your web app. You don't even need a backend. You get the full "Web3" experience (sign in with a blockchain account) with our "Web2" compatible stack (see: [Broken link](broken-reference "mention")).

## Capabilities

Using the Xumm SDK in your web project, you get:

* Sign in with a QR code for when loaded on a desktop
* Deeplink (redirect to Xumm, back to your web app) on mobile
* Basic user information: XRP Ledger account address, icon (hashicon or even avatar), connected chain (mainnet, testnet, ..) & some basic information about the end user's environment (currency, language, ...)
* An access token (JSON Web Token "JWT") valid for 24h, to actively send (push) Sign Requests (transactions for the end user to sign)

## Sample code

{% hint style="info" %}
Please note the **`xumm.authorize()`** and **`xumm.logout()`** methods:
{% endhint %}

{% code lineNumbers="true" %}
```html
<html lang="en">
  <body>
    <h1 id="accountaddress">...</h1>
    <button id="signinbutton" onclick="xumm.authorize()">Login</button>
    <button id="logoutbutton" onclick="xumm.logout()">Logout</button>
        
    <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
    <script>
      var xumm = new Xumm('your-api-key')
      
      xumm.on("ready", () => console.log("Ready (e.g. hide loading state of page)"))
      
      // We rely on promises in the `success` event: fired again if a user
      // logs out and logs back in again (resets all promises)
      xumm.on("success", async () => {
        xumm.user.account.then(account => {
          document.getElementById('accountaddress').innerText = account
        })
      })

      xumm.on("logout", async () => {
        document.getElementById('accountaddress').innerText = '...'
      })
    </script>
  </body>
</html>
```
{% endcode %}

### More links

For the SDK documentation (objects, methods), see the SDK section: [sdk-syntax](../../js-ts-sdk/sdk-syntax/ "mention"). For a simple demo of the Xumm SDK in a React Native environment, check this sample repository: [https://github.com/XRPL-Labs/XummSDK-React-Demo](https://github.com/XRPL-Labs/XummSDK-React-Demo/)

