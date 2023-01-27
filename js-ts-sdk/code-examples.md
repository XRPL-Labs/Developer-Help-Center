# Code examples

{% tabs %}
{% tab title="Typescript (Backend)" %}
{% code lineNumbers="true" %}
```typescript
import { Xumm } from "xumm";

try {
  const Sdk = new Xumm(process.env.XUMM_KEY, process.env.XUMM_SECRET);
  const pong = await Sdk?.ping();
  const payload = await Sdk.payload?.create({
    custom_meta: {
      instruction: "Sign request from " + pong?.application.name,
    },
    txjson: {
      TransactionType: "SignIn",
    }
} catch (e) {
  console.log("Error:", (e as Error).message);
}
```
{% endcode %}

#### See this code in action:

{% embed url="https://codesandbox.io/p/sandbox/xumm-sdk-6gm4du" %}
{% endtab %}

{% tab title="Javascript (Browser)" %}

{% endtab %}
{% endtabs %}
