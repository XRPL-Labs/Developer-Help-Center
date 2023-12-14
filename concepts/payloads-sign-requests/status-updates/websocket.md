---
description: Websockets provide real-time payload updates
---

# Websocket

All payloads get assigned a payload-specific Websocket URL. You can connect to this socket from the client side of your application to receive live status updates (if the user opens the payload on their device and the user resolves the payload).

The pushed information contains minimal information; it is meant to trigger your application to fetch more information from your application's backend.

If a payload doesn't exist, the Websocket connection will receive an `{"message":"..."}` update, and the socket will be closed. If the payload has expired, the connection will receive a `{"expired":true"}` message.

If the payload exists and did not expire, the connection will start with a message containing the remaining seconds until expiration: `{"expires_in_seconds":51}`. This message will be sent every 15 seconds for keepalive reasons. If the connection is still active when the payload expires, a `{"expired":true"}` message will be sent. The connection will be kept alive, leaving it up to the client to disconnect.

## Expiration

The expiration should be handled as an **OPEN/SCAN BEFORE**, not a **RESOLVE BEFORE**. If the end user opens the payload (from the push notification, deep link, or QR scanning) but it didn't resolve before expiration, they will not receive a notification and will still be able to resolve it as if the payload hadn't expired.

When the user resolves after the expiration moment, the webhook and callback will handle the response as they would when the payload wasn't expired.

## Websocket Events

**Websocket events to expect**

<table><thead><tr><th width="348">Event</th><th>JSON</th></tr></thead><tbody><tr><td>Connected</td><td><code>{"message":"Welcome &#x3C;payload-uuid>"}</code></td></tr><tr><td>After connecting and every 15 seconds while the connection is alive, a negative value means the transaction expired that many seconds ago</td><td><code>{"expires_in_seconds":54}</code></td></tr><tr><td>When the user received the payload, eg. push notification, deeplink or QR scan</td><td><code>{"opened":true}</code></td></tr><tr><td>When the Xumm SDK/API fetched the payload details</td><td><code>{"devapp_fetched":true}</code></td></tr><tr><td>When the user starts the signing routine</td><td><code>{"pre_signed":true}</code></td></tr><tr><td>When the submission to a node starts</td><td><code>{"dispatched":true}</code></td></tr><tr><td>When the payload is resolved</td><td><code>{"payload_uuidv4": "...", [...] }</code><br>With: <code>signed: true/false</code></td></tr><tr><td>When the payload is expired</td><td><code>{"expired":true}</code></td></tr></tbody></table>

{% hint style="warning" %}
**WARNING! Do not just rely on a \`signed: true\` indication! If you receive a websocket message with \`signed: true\` indication, always fetch the payload to confirm that all payment details are as expected.**
{% endhint %}

## Sample

The Websocket payload resolve message looks like:

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
The payload information the Websocket connection delivers **does not contain** the entire payload object. It should be considered a trigger to **GET** the entire payload using an SDK/API call: [get.md](../../../js-ts-sdk/sdk-syntax/xumm.payload/get.md "mention")
{% endhint %}
