---
description: Scan a QR code
---

# scanQr()

## Syntax

```javascript
xumm.xapp.scanQr()
xumm.xapp.on('qr', data => {
    console.log('QR', data)
})
```

## Response

Returns an event: `qr`. Use [on-event-fn.md](on-event-fn.md "mention") to subscribe to the return data.
