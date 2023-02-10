---
description: >-
  Certain events are sent to xApps. These events are usually an asynchronous
  callback containing data requested by calling one of the xApp UI actions.
---

# on(event, fn)

To subscribe to one of the events emitted to xApps, use the `on(...)` method on the SDK's `xapp` object to register an event handler (callback function).

## payload

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
  "reason": "DECLINED"
}
```
{% endtab %}

{% tab title="Response: declined" %}
```json
{
  "reason": "SIGNED"
}
```
{% endtab %}
{% endtabs %}

## qr

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

## destination

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

