# WebSocket

All payloads get assigned a payload specific websocket URL. You can connect to this socket from the client side of your application to receive live status updates (if the user opened the payload on their device, and the user resolved the payload).

The pushed information contains minimal information; it is meant to trigger your application to fetch more information from your application's backend.

If a payload doesn't exist, the websocket connection will receive a `{"message":"..."}` update and the socket will be closed. If the payload has expired, the connection will receive an `{"expired":true"}` message.

If the payload exists and did not expire, the connection will start with a message containing the remaining seconds until expiration: `{"expires_in_seconds":51}`. This message will be sent every 15 seconds for keepalive reasons. If the connection is still active when the payload expired, an `{"expired":true"}` message will be sent. The connection will be kept alive though, leaving it up to the client to disconnect.

## Expiration

The expiration should be handled as a **OPEN/SCAN BEFORE**, not a **RESOLVE BEFORE**. If the end user opens the payload (from the push notification, deeplink or QR scanning) but it didn't resolve before expiration, they will not receive a notification, and will still be able to resolve as if the payload hadn't expired.

When the user resolves after the expiration moment, the webhook and callback will handle the response as they would when the payload wasn't expired.

## WebSocket Events

**WebSocket events to expect**

| Event                                                                                                                                     | JSON                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| Connected                                                                                                                                 | `{"message":"Welcome <payload-uuid>"}` |
| After connecting and every 15 seconds while the connection is alive, a negative value means the transaction expired that many seconds ago | `{"expires_in_seconds":54}`            |
| When the user received the payload, eg. push notification, deeplink or QR scan                                                            | `{"opened":true}`                      |
| When the Xumm SDK/API fetched the payload details                                                                                         | `{"devapp_fetched":true}`              |
| When the payload is resolved                                                                                                              | `{"payload_uuidv4": "...", [...] }`    |
| When the payload is expired                                                                                                               | `{"expired":true}`                     |

## Sample

The WebSocket payload resolve message looks like:

```json
{
  "payload_uuidv4": "<some-uuid>",
  "reference_call_uuidv4": "<some-uuid>",
  "return_url":{
    "app": "<some-url>",
    "web": "<some-url>",
  },
  "signed": true,
  "opened_by_deeplink": false,
  "user_token": true,
  "custom_meta":{
    "identifier": "<some-identifier>",
    "blob": {},
    "instruction": "<some-instruction>"
  },
  "txid": "<some-tx-hash>"
}
```

{% hint style="info" %}
The payload information the WebSocket connection delivers **does not contain** the entire payload object. It should be considered a trigger to **GET** the entire payload using an SDK/API call: [get-....md](../../../js-ts-sdk/sdk-syntax/xumm.payload-.../get-....md "mention")
{% endhint %}
