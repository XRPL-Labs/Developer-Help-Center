---
description: >-
  A sign request in Xumm is a prompt to approve a transaction or action on the
  XRP Ledger. This page will show you how you can create a Sign Request, and how
  you can deliver the request to the end user.
---

# Sign Request (payload)

## Browser ("Web3")

...

## xApps ("dApps")

xApps are natively aware of the end user context, so a Sign Request payload can easily be served with the `xumm.xapp.openSignRequest` method: [opensignrequest-....md](../sdk-ts-js/xumm.xapp-.../opensignrequest-....md "mention")

{% tabs %}
{% tab title="TypeScript/MJS" %}
```typescript
const payload = await xumm.payload?.create({
  TransactionType: "Payment",
  Destination: "rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ",
  Amount: "1000",
})

xumm.xapp?.openSignRequest(payload)
```
{% endtab %}

{% tab title="JavaScript (Client side)" %}
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
          TransactionType: "Payment",
          Destination: "rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ",
          Amount: "1000",
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
{% endtabs %}

## Backend (SDK)

...

## Backend (API)

...
