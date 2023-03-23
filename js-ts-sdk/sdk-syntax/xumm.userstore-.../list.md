---
description: List userstore keys
---

# list()

The Xumm **userstore** allows you to store key/value records specific to your application and the user for which the JWT was issued. The **userstore** stays does not expire, meaning you can permanently store userdata and retrieve it whenever the user visits again.

**The \`list\` method returns a Promise with an array of keys stored.**

```javascript
xumm.userstore.list().then(storedKey => {
  console.log(storedKey)
})
```
