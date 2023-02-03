---
description: >-
  Building a web app? Running as a client side SPA (single page webapp) or
  server side rendered? React Native / VueJS / VanillaJS / etc.: you can
  integrate with the Xumm ecosystem using our SDK.
---

# Client side web apps "Web3"

The Xumm SDK can run fully client side: either as part of your compiled web app or using plain HTML and Javascript using our ready to use [browserified](https://xumm.app/assets/cdn/xumm.min.js) version.

Using the Xumm SDK, you can easily add "Sign in with Xumm" capabilities to your web app. You don't even need a backend. You get the full "Web3" experience (sign in with a blockchain account) with our "Web2" compatible stack (see: [xumm-as-identity-provider.md](xumm-as-identity-provider.md "mention")).

## Capabilities

Using the Xumm SDK in your web project, you get:

* Sign in with a QR code for when loaded on a desktop
* Deeplink (redirect to Xumm, back to your web app) on mobile
* Basic user information: XRP Ledger account address, icon (hashicon or even avatar), connected chain (mainnet, testnet, ..) & some basic information about the end user's environment (currency, language, ...)
* An access token (JSON Web Token "JWT") valid for 24h, to actively send (push) Sign Requests (transactions for the end user to sign)

## Demo

Several implementations are available here:

{% embed url="https://oauth2-pkce-demo.xumm.dev/" %}
Xumm Web Sign In & Sign Request demo
{% endembed %}

{% tabs %}
{% tab title="Vanilla JS" %}
A "VanillaJS" implementation sample as demonstrated [here](https://oauth2-pkce-demo.xumm.dev/jsmodule-payload):

{% code title="index.html" lineNumbers="true" %}
```html
<html lang="en">
  <head>
    <title>Xumm Web3 demo</title>
  </head>
  <body>
    <h2 class="mt-3 h4 alert alert-primary text-center shadow mb-5" id="sub">... (please sign in)</h2>

    <button class="btn mb-3 btn-primary" id="auth">Auth</button>
    <button class="btn mb-3 btn-info" style="display: none;" id="signrequest">Sample Payment (Sign request)</button>
    <button class="btn mb-3 btn-danger" style="display: none;" id="logout">Logout</button>

    <script type="module">
      import 'https://xumm.app/assets/cdn/xumm-oauth2-pkce.min.js?v=2.7.1'

      const xumm = new XummPkce('some-apikey', {
        implicit: true, // Implicit: allows to e.g. move from social browser to stock browser
        redirectUrl: document.location.href + '?custom_state=test'
      })
      
      xumm.on("error", error => console.log("error", error))
      xumm.on("success", () => signedIn())
      xumm.on("retrieved", () => signedIn())

      const signedIn = async () => {
        const state = await xumm.state()
        if (state?.me?.sub) {
          document.getElementById('logout').style.display = 'block'
          document.getElementById('signrequest').style.display = 'block'
          document.getElementById('auth').style.display = 'none'
          document.getElementById('sub').innerText = state.me.sub // account address
        }
      }

      document.getElementById('auth').onclick = () => xumm.authorize().catch(e => console.log('e', e))

      document.getElementById('signrequest').onclick = async () => {
        const {sdk} = await xumm.state()
        const payload = await sdk.payload.create({
          TransactionType: 'Payment',
          Destination: 'rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ',
          Amount: String(1234567), // 1.234567 XRP (drops, millionth XRP)
        })

        if (payload.pushed) {
          alert('Payload `' + payload.uuid + '` pushed to phone.')
        } else {
          alert('Payload not pushed, opening payload...')
          window.open(payload.next.always)
        }
      }

      document.getElementById('logout').onclick = () => {
        xumm.logout()

        document.getElementById('logout').style.display = 'none'
        document.getElementById('signrequest').style.display = 'none'
        document.getElementById('auth').style.display = 'block'
        document.getElementById('sub').innerText = '... (please sign in)'
      }
    </script>
  </body>
</html>
```
{% endcode %}
{% endtab %}

{% tab title="React" %}
See this sample repository:

{% embed url="https://github.com/XRPL-Labs/XummSDK-React-Demo" %}
{% endtab %}
{% endtabs %}
