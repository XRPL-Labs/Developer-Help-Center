---
description: Set userstore value (object) for key
---

# set( ..., { ... } )

The Xumm **userstore** allows you to store key/value records specific to your application and the user for which the JWT was issued. The **userstore** stays does not expire, meaning you can permanently store userdata and retrieve it whenever the user visits again.

{% hint style="info" %}
The Xumm userstore data is stored at the Xumm patform **backend**, and is unique to the combination of your app and the user's device. The userstore **does persist** across xApp loads, even if the user clears the local device browser cache.&#x20;
{% endhint %}

**The value (second argument) must be an object.**

```javascript
xumm.userstore.set('userdetails', { name: 'Jane', gender: 'F' })
```
