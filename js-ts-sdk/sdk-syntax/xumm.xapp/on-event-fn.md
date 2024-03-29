---
description: >-
  Certain events are sent to xApps. These events are usually an asynchronous
  callback containing data requested by calling one of the xApp UI actions.
---

# on(xAppEvent, fn)

To subscribe to one of the events emitted to xApps, use the `on(...)` method on the SDK's `xapp` object to register an event handler (callback function).

## Payload

The `payload` event is emitted when a payload has been resolved (signed / declined)

{% tabs %}
{% tab title="Example" %}
```javascript
// <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
var xumm = new Xumm('your-api-key')

xumm.xapp.on('payload', data => {
  console.log('Payload resolved', data)
})
```
{% endtab %}

{% tab title="Response: signed" %}
```json
{
  "reason": "SIGNED",
  "uuid": "the-payload-uuid"
}
```
{% endtab %}

{% tab title="Response: declined" %}
```json
{
  "reason": "DECLINED",
  "uuid": "the-payload-uuid"
}
```
{% endtab %}
{% endtabs %}

## QR

The `qr` event is emitted when the QR scanner dialog has been opened, and is now closed. If a QR was scanned the data is returned.

{% tabs %}
{% tab title="Example" %}
```javascript
// <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
var xumm = new Xumm('your-api-key')

xumm.xapp.on('qr', data => {
  console.log('QR scanned (?)', data)
})
```
{% endtab %}

{% tab title="Response: scanned" %}
```json
{
  "qrContents": "the://scanned-qr/contents?...",
  "reason": "SCANNED"
}
```
{% endtab %}

{% tab title="Response: cancelled" %}
```json
{
  "qrContents": null,
  "reason": "USER_CLOSE"
}
```
{% endtab %}

{% tab title="Response: invalid" %}
```json
{
  "qrContents": null,
  "reason": "INVALID_QR"
}
```
{% endtab %}
{% endtabs %}

## Destination

The `destination` event is emitted when the destination picker dialog has been openend, and is now closed. If a destinationw as selected, the data is returned.

{% tabs %}
{% tab title="Example" %}
```javascript
// <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
var xumm = new Xumm('your-api-key')

xumm.xapp.on('destination', data => {
  console.log('Destination account picked (?)', data)
})
```
{% endtab %}

{% tab title="Response: selected" %}
```json
{
  "method": "selectDestination",
  "destination": {
    "address": "r...",
    "tag": 123456,
    "name": "Wietse's Savings"
  },
  "info":{
   "blackHole":false,
   "disallowIncomingXRP":false,
   "exist":true,
   "possibleExchange":false,
   "requireDestinationTag":false,
   "risk":"UNKNOWN"
  },
  "reason": "SELECTED"
}
```
{% endtab %}

{% tab title="Response: cancelled" %}
```json
{
  "reason": "USER_CLOSE"
}
```
{% endtab %}
{% endtabs %}

## Network Switch

The user switched the selected **network** in Xumm while present in the xApp, while your xApp settings (Xumm Developer Console) indicate the xApp shouldn't reload but receive an event.\
The event will contain a property `network` with a key referring to a network from the `rails` endpoint, through [getrails.md](../xumm.helpers/getrails.md "mention")or [https://xumm.app/api/v1/jwt/rails](https://xumm.app/api/v1/jwt/rails)

```javascript
// <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
var xumm = new Xumm('your-api-key')

xumm.xapp.on("networkswitch", ({ network }) => {
  xumm.helpers.getRails().then(rails => {
      alert(JSON.stringify(rails?.[network]))
  })
})
```
