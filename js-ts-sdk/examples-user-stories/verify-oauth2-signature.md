---
description: >-
  If you used the Xumm native OAuth2 Sign In ("Web3" sign in), you can fetch the
  corresponding payload to verify the signature as well.
---

# Verify OAuth2 signature

```javascript
xumm.payload?.get('some-payload-uuid').then(payloadResult => { /**/ })
```

If you want the actual blob and signature for the user signed in with the Xumm OAuth2 flow:

1. Get the JWT contents
2. Get the payload from the JWT (that's the Sign In payload)
3. Get that payload with the SDK
4. Check the payload data, the `response.hex` property holds the signed TX Blob

```javascript
xumm.on("success", async () => {
  const { payload_uuidv4 } = await xumm.environment.jwt
  const payloadResult = await xumm.payload?.get(payload_uuidv4)
  console.log(payloadResult)
})
```
