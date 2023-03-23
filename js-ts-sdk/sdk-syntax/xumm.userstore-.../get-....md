---
description: Get userstore value (object) by key
---

# get( ... )

The Xumm **userstore** allows you to store key/value records specific to your application and the user for which the JWT was issued. The **userstore** stays does not expire, meaning you can permanently store userdata and retrieve it whenever the user visits again.

**The \`get\` method returns a promise returning the object stored for the given key.**

```javascript
xumm.userstore.get('userdetails').then(storedObject => ...)
```
