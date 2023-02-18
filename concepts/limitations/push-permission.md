# Push permission

Two types of Push:

1.  Payload (Sign Request Push). **Any application can send Sign Requests with a push notification after the user interacted with the app at least once**.

    1. Backend integration: the Webhook & Payload **get** will contain a **user token** after the user decided to interact by signing a payload.
    2. xApp & Browser (Web3) integrations obtain a user token after xApp open / Sign In.

    \- A **user token** is valid for 30 days (default, can be extended on a per app basis if good reasons are provided). Every time the user interacts with the app again, the 30 day cycle will reset.\
    \- When creating a new payload (sign request), the user token can be specified in the payload, after which the user will receive a push notification, and the sign request will present itself in the Event List of the user.\
    \- Users can revoke the user token validity in Xumm (Settings - 3rd party apps - Revoke)\
    \- A **user token** is user & app bound, meaning the same user token can only be used by the API credentials it was originally extended to.
2. Custom xApp push events. **Custom xApp push events are permissioned.**
   1. Notification with link to xApp
   2. Notification with link to xApp & Event in Event list with link to xApp
