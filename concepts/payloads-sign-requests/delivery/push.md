---
description: >-
  Delivering Sign Requests using a push notification can be a very convenient
  way for end users to interact with your application: they don't even have to
  scan a QR code.
---

# Push

[xapps-dapps](../../../environments/xapps-dapps/ "mention") and [browser-web3](../../../environments/browser-web3/ "mention") are signed in with user context, so payloads created in those environments will automatically be pushed to the signed in user.

If you are building a backend integration, the flow is slightly different.

## Backend

If your application features user sign in (to identify your user) and you obtained a `user_token` from a **previously signed payload from this specific user**, you can add the `user_token` to the next payload to deliver the payload through a push notification.

The first interaction (to obtain the `user_token`) will always involve either: showing a QR code for the user to scan with the **Xumm** app or a deep link to the **Xumm** app, to sign a payload.

A payload containing a user token looks like this:

```json
{
  "user_token": "c5bc4ccc-28fa-4080-b702-0d3aac97b993",
  "txjson": { ... }
}
```

After posting the payload the the Xumm SDK/API, the response will confirm push notification delivery:

```json
{
  "uuid": "<some-uuid>",
  ...
  "pushed": true
}
```

{% hint style="success" %}
#### User token expiration

The issued user token expires 30 days after the **last** successfully signed payload of your application by the Xumm user, using the same issued user token. If there's a good reason for your application to have longer living user tokens, please contact Xumm Support and explain your use case.
{% endhint %}

## Obtaining the \`user\_token\`

### From a webhook

After the end user resolved the sign request by signing, the configured application Webhook URL will receive a JSON body per POST request, containing the `accessToken` section:

```json
{
  "meta": { ... },
  "payloadResponse": { ... },
  "userToken": {
    "user_token": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    ...
  }
}
```

### From a resolved Payload

When you get the payload results, the `application`.`issued_user_token` contains the user token.

```json
{
  "meta": { ... },
  "application": {
    "issued_user_token": "e5fff0d0-698d-425d-bdcf-3156e744282d",
    ...
  },
  ...
}
```
