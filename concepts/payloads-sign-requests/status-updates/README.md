# Status updates

* Payloads, when interacted with by users, yield real time status updates & have an end result (rejected, signed + signature, etc.)
* Real time status updates show a user interacted with the payload, and give a realtime update when the payload has been resolved. They do not give the resolve data (for security reasons)
  * Use this in your UI for the best experience ("opened", "signed", ...)
  * You can subscribe to the websocket both in your frontend (to keep the user informed) and backend (to determine when you can fetch results)
* Once resolved, a WebHook (HTTP Call) to your platform can be sent, see [webhooks](webhooks/ "mention")
* You can also fetch the payload end results using API/SDK [xumm.payload-...](../../../js-ts-sdk/sdk-syntax/xumm.payload-.../ "mention")
