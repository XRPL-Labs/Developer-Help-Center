---
description: Contact the Xumm platform to check for connectivity and valid auth.
---

# ping()

The `ping` method allows you to verify API access (valid credentials) and returns some info on your XUMM APP:

```typescript
const pong = await Sdk.ping();
```

Returns [`<ApplicationDetails>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Meta/ApplicationDetails.ts):

```javascript
{
  quota: {},
  application: {
    uuidv4: '00000000-1111-2222-3333-aaaaaaaaaaaa',
    name: 'My XUMM APP',
    webhookurl: '',
    disabled: 0
  },
  call: { uuidv4: 'bbbbbbbb-cccc-dddd-eeee-111111111111' }
}
```
