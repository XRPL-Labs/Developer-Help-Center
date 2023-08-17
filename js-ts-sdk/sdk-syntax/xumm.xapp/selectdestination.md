---
description: >-
  Open the Destination Picker: select/find/scan (QR) an XRPL destination account
  by r-address, slug or PayString
---

# selectDestination({ ... })

## Parameters

If you want to request the destination address only, skipping the "Destination Tag" required check & input, you can provide the `ignoreDestinationTag` param. If not provided (or `false`) Xumm will chech if the destination account requires a Destination Tag and ask the user to input one.

```javascript
{ ignoreDestinationTag: boolean }
```

{% hint style="info" %}
The `ignoreDestinationTag` feature is available in Xumm 2.5.0 and higher.
{% endhint %}

## Syntax

```javascript
xumm.xapp.selectDestination({ ignoreDestinationTag: false })
xumm.xapp.on('destination', data => {
    console.log('Destination', data.destination)
})
```

## Response

Returns an event: `destination`. Use [on-event-fn.md](on-event-fn.md "mention") to subscribe to the return data.
