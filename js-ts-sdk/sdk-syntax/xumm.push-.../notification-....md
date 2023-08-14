# notification( ... )

To send a (native) push notification to an end user. When the push notification is tapped, the xApp will open. When the push notification is dismissed, the user can't access this event anymore.

```typescript
async Sdk.Push.notification (
  data: EventPushPostBody
): Promise<PushResponse>
```
