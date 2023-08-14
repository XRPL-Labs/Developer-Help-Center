# Xumm.backendstore { ... }

**App Storage ('backendstore') allows you to store a JSON object at the XUMM API platform, containing max 60KB of data.**&#x20;

{% hint style="info" %}
Your XUMM APP storage is stored at the XUMM API backend, meaning it persists until you overwrite or delete it.
{% endhint %}

{% hint style="warning" %}
This data is private, and accessible only with your own API credentials. This private JSON data can be used to store credentials / config / bootstrap info / ... for your headless application (eg. POS device).
{% endhint %}

```typescript
const storageSet = await Sdk.storage.set({
  name: "Wietse",
  age: 32,
  male: true,
});
console.log(storageSet);
// true

const storageGet = await Sdk.storage.get();
console.log(storageGet);
// { name: 'Wietse', age: 32, male: true }

const storageDelete = await Sdk.storage.delete();
console.log(storageDelete);
// true

const storageGetAfterDelete = await Sdk.storage.get();
console.log(storageGetAfterDelete);
// null
```
