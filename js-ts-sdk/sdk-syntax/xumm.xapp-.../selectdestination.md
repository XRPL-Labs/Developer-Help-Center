---
description: >-
  Open the Destination Picker: select/find/scan (QR) an XRPL destination account
  by r-address, slug or PayString
---

# selectDestination()

## Syntax

```javascript
xumm.xapp.selectDestination()
xumm.xapp.on('destination', data => {
    console.log('Destination', data.destination)
})
```

## Response

Returns an event: `destination`. Use [on-event-fn.md](on-event-fn.md "mention") to subscribe to the return data.
