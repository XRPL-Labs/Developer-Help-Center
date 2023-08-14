# cancel( ... )

To cancel a payload, provide a payload UUID (string), a `<XummPayload>` (by performing a `Sdk.payload.get()` first) or a `<CreatedPayload>` (by using the response of a `Sdk.payload.create()` call). By cancelling an existing payload, the payload will be marked as expired and can no longer be opened by users.

**Please note**: _if a user already opened the payload in XUMM APP, the payload cannot be cancelled: the user may still be resolving the payload in the XUMM App, and should have a chance to complete that process_.

A response (generic API types [here](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/xumm-api/index.ts)) looks like:

```javascript
{
  result: {
    cancelled: boolean;
    reason: XummCancelReason;
  }
  meta: XummPayloadMeta;
  custom_meta: XummCustomMeta;
}
```

### Object

```typescript
async Sdk.payload.cancel (
  payload: string | XummPayload | CreatedPayload,
  returnErrors: boolean = false
): Promise<DeletedPayload | null>
```
