# Code examples

{% tabs %}
{% tab title="TypeScript / ESM (Backend)" %}
{% code lineNumbers="true" %}
```typescript
import { Xumm } from "xumm"

const Sdk = new Xumm(process.env.XUMM_KEY, process.env.XUMM_SECRET)
const pong = await Sdk?.ping()
const payload = await Sdk.payload?.create({
  custom_meta: {
    instruction: "Sign request from " + pong?.application.name,
  },
  txjson: {
    TransactionType: "SignIn",
  },
})

console.log(payload)
```
{% endcode %}

####

#### See this code in action:

{% embed url="https://codesandbox.io/p/sandbox/xumm-sdk-6gm4du?file=/src/index.ts" %}
{% endtab %}

{% tab title="Javascript / CJS (Backend)" %}
```javascript
const { Xumm } = require("xumm")

const Sdk = new Xumm(process.env.XUMM_KEY, process.env.XUMM_SECRET)
Sdk.ping().then(pong => {
  Sdk.payload.create({
    custom_meta: {
      instruction: "Sign request from " + pong.application.name,
    },
    txjson: {
      TransactionType: "SignIn",
    }
  }).then(payload => {
    // Done
    console.log(payload)
  })
})
```
{% endtab %}

{% tab title="Browser" %}
```javascript
const Sdk = new Xumm('some-api-key')

Sdk.authorize()

Sdk.on("ready", () => {
  Sdk.ping().then(pong => {
    Sdk.payload.create({
      custom_meta: {
        instruction: "Sign request from " + pong.application.name,
      },
      txjson: {
        TransactionType: "SignIn",
      }
    }).then(payload => {
      // Done
      console.log(payload)
    })
  })
})
```
{% endtab %}
{% endtabs %}
