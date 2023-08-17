# create( ... )

To create a payload, a `txjson` XRPL transaction can be provided. Alternatively, a transaction formatted as HEX blob (string) can be provided in a `txblob` property. **See the intro for more information about payloads.** Take a look at the [Developer Docs for more information about payloads](https://xumm.readme.io/docs/your-first-payload).

The response of a `Sdk.payload.create()` operation, looks like this:

```json
{
  "uuid": "1289e9ae-7d5d-4d5f-b89c-18633112ce09",
  "next": {
    "always": "https://xumm.app/sign/1289e9ae-7d5d-4d5f-b89c-18633112ce09",
    "no_push_msg_received": "https://xumm.app/sign/1289e9ae-7d5d-4d5f-b89c-18633112ce09/qr"
  },
  "refs": {
    "qr_png": "https://xumm.app/sign/1289e9ae-7d5d-4d5f-b89c-18633112ce09_q.png",
    "qr_matrix": "https://xumm.app/sign/1289e9ae-7d5d-4d5f-b89c-18633112ce09_q.json",
    "qr_uri_quality_opts": ["m", "q", "h"],
    "websocket_status": "wss://xumm.app/sign/1289e9ae-7d5d-4d5f-b89c-18633112ce09"
  },
  "pushed": true
}
```

The `next.always` URL is the URL to send the end user to, to scan a QR code or automatically open the XUMM app (if on mobile). If a `user_token` has been provided as part of the payload data provided to `Sdk.payload.create()`, you can see if the payload has been pushed to the end user. A button "didn't receive a push notification" could then take the user to the `next.no_push_msg_received` URL. The

Alternatively user routing / instruction flows can be custom built using the QR information provided in the `refs` object, and a subscription for live status updates (opened, signed, etc.) using a WebSocket client can be setup by connecting to the `refs.websocket_status` URL. **Please note: this SDK already offers subscriptions. There's no need to setup your own WebSocket client:** [createandsubscribe.md](createandsubscribe.md "mention")

### Object

```typescript
async Sdk.payload.create (
  payload: CreatePayload,
  returnErrors: boolean = false
): Promise<CreatedPayload | null>
```
