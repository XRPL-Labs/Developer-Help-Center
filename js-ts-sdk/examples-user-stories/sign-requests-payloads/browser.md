---
description: >-
  A sign request in Xumm is a prompt to approve a transaction or action on the
  XRP Ledger. This page will show you how you can create a Sign Request, and how
  you can deliver the request to the end user.
---

# Browser

When working with Xumm sign in & payloads in the browser, there are **two flows to consider.** Your application should deal with both flows.

* User is on **mobile**, Xumm is installed
* User is on **desktop**, Xumm is on their phone

### Mobile

When a user visits on their smartphone with Xumm installed, your application can "deeplink" straight into Xumm, where a Sign Request will be opened.

{% hint style="info" %}
* If your application can persist state, you can use a return URL to get your user to return to your web app.
* If you need the user to return to the launching webpage, do not provide a return URL to the payload, so the user is forced to go back to the launching browser.
{% endhint %}

To make sure the user is expecting Xumm to open, the best user experience would be to ask the user to open Xumm (with a button), alternatively allowing them to use a button to just show the QR code, so the Sign Request can be opened on another device.

{% hint style="info" %}
For more information about the object contents to be used for Payloads & the return URL replacement variables, see: [https://xumm.readme.io/reference/post-payload](https://xumm.readme.io/reference/post-payload)
{% endhint %}

{% tabs %}
{% tab title="Promise" %}
```javascript
xumm.payload.create({
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
}).then(payload => {
  // Redirect directly to payload.next.always, or (preferable)
  var btn = document.getElementById('launchXummBtn')
  btn.setAttribute('href', payload.next.always)
})
```
{% endtab %}

{% tab title="Async" %}
```typescript
const paload = await xumm.payload.create({
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

// Now assigin the link to a button or redirect the user straight away to:
// payload.next.always
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Warning: most mobile browsers / operating systems **will only** allow deeplinks to trigger an application (so: the payload URL to trigger opening Xumm) if the button resulting in the trigger is **user invoked**.

Meaning there must always be a direct user onclick/ontap event resulting in the routine opening the payload URL being opened will deeplink.
{% endhint %}

### Desktop

On the desktop, a user may or may not receive a push notification. The user can scan a QR code as fallback. The ideal implementation:

1. Checks if the `pushed` property of the created payload
   1. If `false` the user is displayed the payload QR code to scan with their phone.
      1. Using the [createandsubscribe.md](../../sdk-syntax/xumm.payload/createandsubscribe.md "mention") method the application receives real time updates about end user interaction. The application can update to reflect the interaction the user has with the Sign Request on their phone (`"opened": true`).
   2. If `true` the user is displayed a message that the Sign Request has been delivered to their phone. A button with a label like **"I did not receive the Push Notification**" is displayed, which takes users to the QR flow.

{% tabs %}
{% tab title="Promise" %}
```javascript
xumm.payload.createAndSubscribe({
  TransactionType: 'Payment',
  Destination: 'rfHn6cB5mmqZ6fHZ4fdemCDSxqLTijgMwo',
  Amount: String(1000000) // one million drops, 1 XRP
}, eventMessage => {
  if ('opened' in eventMessage.data) {
    // Update the UI? The payload was opened.
  }
  if ('signed' in eventMessage.data) {
    // The `signed` property is present, true (signed) / false (rejected)
    return eventMessage
  }
})
  .then(({ created, resolved }) => {
    console.log('Payload URL:', created.next.always)
    console.log('Payload QR:', created.refs.qr_png)

    return resolved // Return payload promise for the next `then`
  })
  .then(payload => console.log('Payload resolved', payload))
  // This is where you can do `xumm.payload.get(...)` to fetch details
```
{% endtab %}

{% tab title="Async" %}
```typescript
const { created, resolved } = await xumm.payload.createAndSubscribe({
  TransactionType: 'Payment',
  Destination: 'rfHn6cB5mmqZ6fHZ4fdemCDSxqLTijgMwo',
  Amount: String(1000000) // one million drops, 1 XRP
}, eventMessage => {
  if ('opened' in eventMessage.data) {
    // Update the UI? The payload was opened.
  }
  if ('signed' in eventMessage.data) {
    // The `signed` property is present, true (signed) / false (rejected)
    return eventMessage
  }
})

console.log('Payload URL:', created.next.always)
console.log('Payload QR:', created.refs.qr_png)

const payload = await resolved

console.log('Resolved', payload)
```
{% endtab %}
{% endtabs %}
