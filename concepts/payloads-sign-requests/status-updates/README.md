---
description: >-
  Xumm's Payload status updates bridge the gap between your application and the
  end user by providing real-time feedback on payload interactions.
---

# Status updates

### Overview

When users interact with payloads, Xumm provides real-time status updates and results (e.g., rejected, signed with signature). These updates allow you to make your application user interface reflect the status of the interaction with the user, and return sign request results to your application.

### Real-Time Status Updates

* Keep track of user interactions with the payload.
* Update the UI to reflect statuses like "opened" or "signed".
* They provide status but not the final resolved data (for security reasons, resolved data like signatures can only be separately fetched from the Xumm platform).

### Websocket Usage

* Receive real-time updates in your front-end and back-end.
* **Frontend**: Keep the user informed about the status.
* **Backend**: Determine when you can fetch final results.
* This ensures responsiveness and keeps the end-user informed.

### Fetching End Results

* **Webhook**: Once the payload is resolved, a Webhook can be sent to your platform for backend processing. For more on WebHooks, see [webhooks](webhooks/ "mention").
* **API/SDK**: Alternatively, fetch the payload end results using the Xumm API or SDK  [xumm.payload](../../../js-ts-sdk/sdk-syntax/xumm.payload/ "mention") for more control and flexibility.

### Status Updates for End users

Understanding the end user's workflow/experience is vital. The real-time status updates and Webhooks are not just technical tools but communication channels between your application and the user.&#x20;

By effectively using these features, you ensure an engaging and informed experience for the user.
