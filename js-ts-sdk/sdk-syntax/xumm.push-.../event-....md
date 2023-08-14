# event( ... )

To send a push notification & publish an xApp Event in the Event List of the end user. When tapped, the xApp opens. When the push notification is tapped, the xApp will open. When the push notification is dismissed, the user can still find it in the XUMM Event list.

```typescript
async Sdk.Push.event (
  data: EventPushPostBody
): Promise<EventResponse>
```
