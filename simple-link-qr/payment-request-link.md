---
description: >-
  To route users to a simple payment request, all you need to use is a URL / QR
  containing that URL, crafted with the right parameters.
---

# Payment Request Link

To offer users a direct payment link, you can send them straight to a URL (deeplink) or QR containing that same URL. The URL already contains destination, network, currency & other parameters.

{% hint style="info" %}
Note: Payment Requests will request for the given asset to be **delivered** to the given destination account. The Xaman user will be offered an interface where they can choose to send any asset they own that can satisfy delivering the requested amount. This means that if you verify the transaction recieved, you must take into account that the transaction can contain an asset sent by the user that differs from the asset delivered to you.
{% endhint %}

## Example URLs

A simple payment on Xahau for 2 XAH (native asset) to the `rwietse...` account:

[https://xaman.app/detect/request:rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XAHAU\
](https://xaman.app/detect/request:rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XAHAUhttps://xaman.app/detect/request:rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XRPL\&dt=123\&issuer=rMxCKbEDwqr76QuheSUMdEGf4B9xJ8m5De\&currency=524C555344000000000000000000000000000000)

A payment on the XRP Ledger for 2 $RLUSD to the `rwietse...` account:[\
https://xaman.app/detect/request:rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XRPL\&dt=123\&issuer=rMxCKbEDwqr76QuheSUMdEGf4B9xJ8m5De\&currency=524C555344000000000000000000000000000000](https://xaman.app/detect/request:rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XAHAUhttps://xaman.app/detect/request:rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XRPL\&dt=123\&issuer=rMxCKbEDwqr76QuheSUMdEGf4B9xJ8m5De\&currency=524C555344000000000000000000000000000000)

## Variants (universal)

If the user does not have Xaman installed, the above links will automatically fall back to a regular webpage showing the payment request information & download links to Xaman. If you however want to craft a link / QR that is not Xaman specific, you can use a **protocol** prefix which can be claimed by any XRPL supporting app in the ecosystem. The downside is that if one does not have a supporting app installed, there is no graceful fallback webpage.

Instead of prefixing with `https://xaman.app/detect/request` you can prefix with the `xrpl://` protocol handler:

[xrpl://rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XRPL\&dt=123\&issuer=rMxCKbEDwqr76QuheSUMdEGf4B9xJ8m5De\&currency=524C555344000000000000000000000000000000\&invoiceid=0CAFEBABE000DEADBEEF000CAFEBABE000DEADBEEF000CAFEBABE000DEADBEEF](xrpl://rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ?amount=2\&network=XRPL\&dt=123\&issuer=rMxCKbEDwqr76QuheSUMdEGf4B9xJ8m5De\&currency=524C555344000000000000000000000000000000\&invoiceid=0CAFEBABE000DEADBEEF000CAFEBABE000DEADBEEF000CAFEBABE000DEADBEEF)

## Parameters

* `amount` - The amount in native asset or issued currency to request - **can be omitted, the user can then enter the amount**
* `network` - The network the transaction should be sent on, can be `XRPL` or `XAHAU`, can be omitted, defaults to `XRPL`
* `dt` - The Destination Tag to send to - can be omitted
* `invoiceid` - The InvoiceID to send, must be formatted in HEX according to the InvoiceID length specifications (64 hex chars) - usually omitted
* `issuer` - The issuing account, only required combined with `currency` for requests in issued currencies
* `currency` - The currency code, must be in three-char ALPHA notation or HEX notation for issued currencies with asset codes > 3 char length. Only required in combination with `issuer` for payments in issued assets.
