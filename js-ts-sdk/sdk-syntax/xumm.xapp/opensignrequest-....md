---
description: Open a Sign Request (payload) created with Xumm.payload.create
---

# openSignRequest({ ... })

## Parameters

```javascript
{ uuid: '...' }
```

## Syntax

```javascript
xumm.payload.create({
  TransactionType: 'Payment',
  Destination: 'rfHn6cB5mmqZ6fHZ4fdemCDSxqLTijgMwo',
  Amount: String(1)
}).then(payload => {
  xumm.xapp.openSignRequest(payload)
})
```

## Response

Returns an event: `payload`. Use [on-event-fn.md](on-event-fn.md "mention") to subscribe to the return data.
