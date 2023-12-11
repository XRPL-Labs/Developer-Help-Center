---
description: Navigate to another xApp (by identifier)
---

# navigate({ … })

{% hint style="warning" %}
Warning! This command is **permissioned**. To use it in your xApp, please contact Xumm[ Support](https://xumm.app/detect/xapp:xumm.support-md), explain the user flow & use case and share your API key so we can discuss granting your xApp this permission.
{% endhint %}

## Parameters

```javascript
{ xApp: '...' }
```

The provided value of the `xApp` property should be a valid xApp identifier.

## Syntax

```javascript
xumm.xapp.navigate({ xApp: 'xumm.support' })
```
