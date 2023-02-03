---
description: >-
  To prevent excessive load on our platform, the Xumm platform applies rate
  limits. The limits depend on the type of consumer (regular API, SDK, JWT) and
  endpoint(s).
---

# Rate limits

On average, the Xumm platform allows API consumers to make between 60\~200 calls per minute. These numbers depend on the load on the platform and the use of the API consumer.

Some endpoints have lower limits, e.g.:

* POST a Payload (sign request) on average allows for sending **30** payloads per minute
* Fetching TXs (no need to use our platform, best use a native XRPL WebSocket connection): **60** requests per minute
* KYC status: **600** calls per minute
* Account metadata: **120** calls per minute

{% hint style="info" %}
To make sure you are not hitting the API limits, every call to our API returns two response headers:

* `X-RateLimit-Limit` (e.g.: 30)
* `X-RateLimit-Remaining` (e.g. 21)

These headers return the results of the current requests allowed per minute, and the amount remaining in the current (sliding) minute.
{% endhint %}

These numbers are not guarantees: they are averages and can be adjusted by our platform on the fly, based on your overall API call behaviour & end user interaction(s).

## Raising API limits

If there are good reasons to assign elevated API limits, we're happy to have a discussion to hear about the reasons how your application consumes the Xumm API, and why your application needs higher limits. Please [contact Xumm Support](https://xumm.app/detect/xapp:xumm.support).\
