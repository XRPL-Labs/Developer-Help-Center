---
description: >-
  Use your API key and secret obtained from the Xumm Developer Console & off you
  go. Using our SDK's, or building your own integration on top of our well
  documented APIs.
---

# Backend (SDK / API)

Backend integration intro here...

## Sample code

{% tabs %}
{% tab title="Typescript" %}
```typescript
import { Xumm } from "xumm";

const xumm = new Xumm("some-api-key", "some-secret-key");

(async () => {
  console.log("pong", await xumm.ping());

  const transaction = { TransactionType: "SignIn" };
  console.log("payload", await xumm.payload?.create(transaction)) 
})()
```
{% endtab %}

{% tab title="Javascript (nodejs)" %}
```javascript
const { Xumm } = require('xumm')

const xumm = new Xumm('apikey', 'apisecret')

xumm.ping().then(pong => console.log(pong))

const transaction = { TransactionType: "SignIn" }
xumm.payload?.create(transaction).then(payload => console.log(payload))
```
{% endtab %}
{% endtabs %}
