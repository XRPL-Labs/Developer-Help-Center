---
description: Open an external URL in the OS default browser
---

# openBrowser({ … })

{% hint style="info" %}
Calling the `openBrowser` method will trigger a dialog for the end user to confirm leaving Xumm & opening a browser page. Only under certain conditions this confirmation dialog can be waived on a per xApp, per developer basis.
{% endhint %}

## Parameters

```javascript
{ url: '...' }
```

## Syntax

```javascript
xumm.xapp.openBrowser({ url: 'https://wietse.com' })
```
