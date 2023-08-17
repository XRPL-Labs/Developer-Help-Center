---
description: Close the xApp
---

# close({ ... })

## Parameters

The `refreshEvents` param. is optional. If passed (and `true`) the Event list will be forcefully refreshed (updated) when the xApp closes. This can be useful if the xApp closes programatically after e.g. resolving (cancelling) or signing a Sign Request.

```javascript
{ refreshEvents: true }
```

## Syntax

```javascript
xumm.xapp.close({ refreshEvents: true })
```
