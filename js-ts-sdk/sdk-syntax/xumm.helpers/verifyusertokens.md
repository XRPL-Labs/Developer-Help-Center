---
description: >-
  Verify a user token (or multiple), to see if the token is still valid (not
  expired, not revoked) and can be used to deliver sign requests to user(s)
---

# verifyUserTokens(\[ … ])

The `verifyUserTokens` (or single token: `verifyUserToken`) method allows you to verify one or more User Tokens obtained from previous sign requests. This allows you to detect if you will be able to push your next Sign Request to specific users.

```typescript
const someToken = '691d5ae8-968b-44c8-8835-f25da1214f35')

const tokenValidity = Sdk.verifyUserTokens([
  someToken,
  'b12b59a8-83c8-4bc0-8acb-1d1d743871f1',
  '51313be2-5887-4ae8-9fda-765775a59e51'
])

if ((await Sdk.verifyUserToken(someToken).active) {
  // Push, use `user_token` in payload
} else {
  // QR or Redirect (deeplink) flow
}
```

Returns: [`Promise<UserTokenValidity[]>` or Promise](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Meta/UserTokens.ts)
