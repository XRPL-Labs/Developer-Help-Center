---
description: Remove userstore key & value by key
---

# delete( ... )

The Xumm **userstore** allows you to store key/value records specific to your application and the user for which the JWT was issued. The **userstore** stays does not expire, meaning you can permanently store userdata and retrieve it whenever the user visits again.

```javascript
xumm.userstore.delete('somekey')
```
