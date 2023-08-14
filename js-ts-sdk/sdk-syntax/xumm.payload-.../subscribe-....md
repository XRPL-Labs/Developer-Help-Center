# subscribe( ... )

* Returning non-void in the _callback function_ passed to the `Sdk.payload.subscribe()` method
* Manually calling `<PayloadSubscription>.resolve()` on the object returned by the `Sdk.payload.subscribe()` method

The subscription will be closed by either:

Status updates can be processed by providing a _callback function_ to the `Sdk.payload.subscribe()` method. Alternatively, the (by the `Sdk.payload.subscribe()` method) returned raw websocket can be used to listen for WebSocket `onmessage` events.

More information about the status update events & sample event data: [status-updates](../../../concepts/payloads-sign-requests/status-updates/ "mention")

* The payload is opened by a XUMM App user (webpage)
* The payload is opened by a XUMM App user (in the app)
* Payload expiration updates (remaining time in seconds)
* The payload was resolved by rejecting
* The payload was resolved by accepting (signing)

To subscribe to live payload status updates, the XUMM SDK can setup a WebSocket connection and monitor live status events. Emitted events include:

### Payload subscriptions: live updates

If a callback function is not provided, the subscription will stay active until the `<PayloadSubscription>.resolve()` method is called manually, eg. based on handling `<PayloadSubscription>.websocket.onmessage` events.

When a callback function is provided, for every payload specific event the callback function will be called with [`<SubscriptionCallbackParams>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/651bd409ee2aab47fb9151513b8cf981cc1a4f30/src/types/Payload/SubscriptionCallbackParams.ts).

The `<SubscriptionCallbackParams>.data` property contains parsed JSON containing event information.

Either by calling `<SubscriptionCallbackParams>.resolve()` or by returning a non-void value in the _callback function_ the subscription will be ended, and the `<PayloadSubscription>.resolved` promise will resolve with the value returned or passed to the `<SubscriptionCallbackParams>.resolve()` method.

Resolving (by returning non-void in the callback or calling `resolve()` manually) closes the WebSocket client the XUMM SDK sets up 'under the hood'.

The [`<PayloadSubscription>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Payload/PayloadSubscription.ts) object looks like this:

```javascript
{
  payload: XummPayload,
  resolved: Promise<unknown> | undefined
  resolve: (resolveData?: unknown) => void
  websocket: WebSocket
}
```

### Object

```typescript
async Sdk.payload.subscribe (
  payload: string | XummPayload | CreatedPayload,
  callback?: onPayloadEvent
): Promise<PayloadSubscription>
```
