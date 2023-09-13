---
description: >-
  Get the meta information for all known Hooks. Object returned contains Hook
  hash as key, meta as value.
---

# getHookHashes()

**Sdk.getHookHashes()**

The `getHookHashes` allows you to get all meta information for all Hooks known to Xumm.

```javascript
const hookHashes = await Sdk.getHookHashes();
```

Returns: [`<HookHashes>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Meta/HookHashes.ts)
