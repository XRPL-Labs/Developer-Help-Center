---
description: >-
  xApps are custom applications that run within the Xumm environment. As a
  developer working with xApps, delivering payloads is crucial for a seamless
  user experience.
---

# xApps

### Delivering Payloads within xApps&#x20;

Delivering payloads within xApps is about efficiency and user experience. Since the user is already engaged with your xApp inside Xumm, delivering the payload directly within the xApp streamlines the process. This minimizes context switching for the user and keeps them focused on the task at hand.

### How to Deliver Payloads within xApps

1. **Create a Payload**: First, you need to create a payload with the transaction details. This payload is essentially a sign request you want the user to interact with. See:[sign-requests-payloads](../../../js-ts-sdk/examples-user-stories/sign-requests-payloads/ "mention")
2. **Use Xumm SDK**: To deliver the payload within your xApp, use the Xumm SDK. The SDK provides functions allowing you to seamlessly integrate the payload within your xApp. See: [opensignrequest-....md](../../../js-ts-sdk/sdk-syntax/xumm.xapp-.../opensignrequest-....md "mention")
3. Once integrated, the payload will be displayed to the user within your xApp. The user can then review and interact with the payload without leaving the xApp.
4. **Handle Status Updates**: Implement logic to handle status updates. This includes whether the user signed or rejected the payload. Xumm SDK provides functions that allow you to receive status updates and take appropriate actions based on the user's response, see: [on-event-fn.md](../../../js-ts-sdk/sdk-syntax/xumm.xapp-.../on-event-fn.md "mention")
