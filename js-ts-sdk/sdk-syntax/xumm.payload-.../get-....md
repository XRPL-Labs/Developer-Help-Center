# get( ... )

To get payload details, status and if resolved & signed: results (transaction, transaction hash, etc.) you can `get()` a payload.

Note! Please don't use _polling_! The XUMM API offers Webhooks (configure your Webhook endpoint in the [Developer Console](https://apps.xumm.dev)) or use a subscription to receive live payload updates (for non-SDK users: [Webhooks](https://xumm.readme.io/docs/payload-status)).

You can `get()` a payload by:

*   Payload UUID

    ```javascript
    const payload = await Sdk.payload.get("aaaaaaaa-bbbb-cccc-dddd-1234567890ab");
    ```
*   Passing a created Payload object (see: Sdk.payload.create)

    ```javascript
    const newPayload: XummTypes.CreatePayload = {txjson: {...}}
    const created: XummTypes.CreatedPayload = await Sdk.payload.create(newPayload)
    const payload: XummTypes.XummPayload = await Sdk.payload.get(created)
    ```

If a payload can't be fetched (eg. doesn't exist), `null` will be returned, unless a second param (boolean) is provided to get the SDK to throw an Error in case a payload can't be retrieved:

```javascript
await Sdk.payload.get("aaaaaaaa-bbbb-cccc-dddd-1234567890ab", true)
```

### Object

```typescript
async Sdk.payload.get (
  payload: string | CreatedPayload,
  returnErrors: boolean = false
): Promise<XummPayload | null>
```
