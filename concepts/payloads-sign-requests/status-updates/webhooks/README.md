---
description: >-
  We can send you a WebHook when a Payload (Sign Request) has been resolved
  (rejected or signed)
---

# Webhooks

If you entered a valid Webhook URL in your Application Settings at the Xumm[ Xumm Developer Console](https://apps.xumm.dev/) your application will receive a HTTP POST containing a JSON body with limited details for the given payload.

Please note a WebHook will **not** contain the entire payload: to get the entire payload you should **GET** the payload using an SDK/API call.

#### A sample webhook looks like this:

```json
{
  "meta": {
    "url": "<your-webhook-endpoint>",
    "application_uuidv4": "<some-uuid>",
    "payload_uuidv4": "<some-uuid>",
    "opened_by_deeplink": true
  },
  "custom_meta": {
    "identifier": "some_identifier_1337",
    "blob": {},
    "instruction": "Hey ❤️ ..."
  },
  "payloadResponse": {
    "payload_uuidv4": "<some-uuid>",
    "reference_call_uuidv4": "<some-uuid>",
    "signed": true,
    "user_token": true,
    "return_url": {
      "app": "<your-url>",
      "web": "<your-url>"
    },
    "txid": "<some-tx-hash>"
  },
  "userToken": {
    "user_token": "<some-token>",
    "token_issued": 1635000000,
    "token_expiration": 1637500000
  }
}
```

If a user token (`userToken`.`user_token`) is issued and you plan on payload delivery using push notifications in the future, your application could/should store the token. See [push.md](../../delivery/push.md "mention")

Use the `payloadResponse`.`payload_uuidv4` to confirm and get payload outcome using an SDK/API call.

{% hint style="info" %}
#### Expected result / retry

If your backend does not respond within 15 seconds, or responds with a non 200 HTTP status code, the Xumm platform will retry the webhook four more times (bringing the max. total attempts at five).

The first retry will take place after 10 seconds. The next after 60 seconds. Then two more retries will take place at a 600 second (10 minute) interval.
{% endhint %}

## Safety

If you want to make sure the WebHook your application received came from the Xumm platform, there are two things you can do:

1. Send a **GET** for the payload to get the full payload using the SDK/API to the Xumm platform
2. Verify the signature we send in a HTTP Header when we deliver the WebHook: [signature-verification.md](signature-verification.md "mention")\
