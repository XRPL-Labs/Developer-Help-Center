---
description: >-
  A sign request in Xumm is a prompt to approve a transaction or action on the
  XRP Ledger. This page will show you how you can create a Sign Request, and how
  you can deliver the request to the end user.
---

# xApp

xApps are natively aware of the end user context, so a Sign Request payload can easily be served with the `xumm.xapp.openSignRequest` method: [opensignrequest.md](../../sdk-syntax/xumm.xapp/opensignrequest.md "mention")

{% hint style="info" %}
For more information about the object contents to be used for Payloads & the return URL replacement variables, see: [https://xumm.readme.io/reference/post-payload](https://xumm.readme.io/reference/post-payload)
{% endhint %}

{% tabs %}
{% tab title="JavaScript (VanillaJS)" %}
```html
<html lang="en">
  <head>
    <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
  </head>
  <body>
    <pre id="payload">...</pre>

    <script>
      var xumm = new Xumm('your-api-key')

      xumm.on('payload', event => {
        document.getElementById('payload').innerHTML = JSON.stringify(event, null, 2)
      })

      xumm.payload
        .create({
          txjson: {
            TransactionType: "Payment",
            Destination: "r...",
            Amount: "1000000"
          },
          options: {
            return_url: {
              app: "https://sample.test/?...",
              web: "https://sample.test/?id={id}"
            },
            force_network: "MAINNET"
          },
          custom_meta: {
            identifier: "123123",
            instruction: "Please sign this to..."
          }
        })
        .then(payload => {
          document.getElementById('payload').innerHTML = JSON.stringify(payload, null, 2)
          xumm.xapp.openSignRequest(payload)
        })
    </script>
  </body>
</html>
```
{% endtab %}

{% tab title="TypeScript / mjs" %}
```typescript
const payload = await xumm.payload?.create({
  txjson: {
    TransactionType: "Payment",
    Destination: "r...",
    Amount: "1000000"
  },
  options: {
    return_url: {
      app: "https://sample.test/?...",
      web: "https://sample.test/?id={id}"
    },
    force_network: "MAINNET"
  },
  custom_meta: {
    identifier: "123123",
    instruction: "Please sign this to..."
  }
})

xumm.xapp?.openSignRequest(payload)
```
{% endtab %}
{% endtabs %}

When a payload (Sign Request) has been created and opened in your xApp, you probably want to be informed if the payload has been signed or rejected, then to check the payload results and act on the results. You can do so by subscribing to the `payload` event, see: [xumm.on-event-fn.md](../../sdk-syntax/xumm.on-event-fn.md "mention")

{% tabs %}
{% tab title="Promise" %}
```javascript
xumm.on('payload', data => {
  if (data?.uuid) {
    xumm.payload.get(data.uuid).then(payload => {
      // Payload contains the full paylaod data
    })
  }
})
```
{% endtab %}

{% tab title="Async" %}
```typescript
xumm.on('payload', data => {
  if (data?.uuid) {
    const payload = await xumm.payload.get(data.uuid)
    // Payload contains the full paylaod data
  }
})
```
{% endtab %}
{% endtabs %}
