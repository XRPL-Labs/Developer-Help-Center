---
description: After a user signs a payload, a user can return to a URL (your website / app).
---

# Payload Return URL

The Return URL (`return_url)` determines where the user is sent when the payload is signed. If none is given, the user will simply be displayed `Close` button in Xumm. Otherwise, the user will be presented a button which launches the Return URL.

{% hint style="warning" %}
**Warning!** iOS and Android **do not allow** the user to return to the browser tab they came from (if your flow starts in a browser). Make sure you restore state based on the payload / session / custom identifier or custom metadata assigned to the payload.
{% endhint %}

## Replacement variables

#### You can add the following replacement tags in your Return URL. They will be replaced with the appropriate values by Xumm.

* `{id}` will be replaced with the xumm payload UUID.
* `{cid}` will be replaced with the optional custom payload identifier.
* `{txid}` will be replaced with the signed transaction hash.
* `{txblob}` will be replaced with the signed transaction HEX blob.

## Routing / origin logic

If both the `app` and `web` return URL values are present, and **if they are identical**, the XUMM platform will execute logic to see if the user is coming from a browser tab (local device or remote, e.g. desktop browser). If so, and **if the origin browser window is still active**, only the origin browser window will redirect, and the app won't. Else (if the browser window is not active anymore) XUMM will redirect to the return URL.

This behaviour prevents a double redirect (both on mobile and on desktop / browser window).

## Sample payload body

```json
{
  "txjson": {
    "TransactionType": "..."
  },
  "options": {
    "return_url": {
      "app": "https://...",
      "web": "https://..."
    }
  }
}
```
