# createAndSubscribe( ... )

The [`<PayloadAndSubscription>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Payload/PayloadAndSubscription.ts) object is basically a [`<PayloadSubscription>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Payload/PayloadSubscription.ts) object with the created payload results in the `created` property:

All information that applies on `Sdk.payload.create()` and `Sdk.payload.subscribe()` applies. [create.md](create.md "mention") / [subscribe.md](subscribe.md "mention")\
\
Differences are:

1. The input for a `Sdk.payload.createAndSubscribe()` call isn't a payload UUID / existing payload, but a payload to create.
2. The response object also contains (`<PayloadAndSubscription>.created`) the response obtained when creating the payload.

### Example code

```javascript
xumm.payload.createAndSubscribe({
  TransactionType: 'Payment',
  Destination: 'rfHn6cB5mmqZ6fHZ4fdemCDSxqLTijgMwo',
  Amount: String(1000000) // one million drops, 1 XRP
}, eventMessage => {
  if (Object.keys(eventMessage.data).indexOf('opened') > -1) {
    // Update the UI? The payload was opened.
  }
  if (Object.keys(eventMessage.data).indexOf('signed') > -1) {
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

### Object

```typescript
async Sdk.payload.createAndSubscribe (
    payload: CreatePayload,
    callback?: onPayloadEvent
  ): Promise<PayloadAndSubscription>
```
