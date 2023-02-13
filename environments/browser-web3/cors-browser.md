---
description: >-
  CORS (Cross-Origin Resource Sharing) is a security feature that restricts a
  web page from accessing resources from another domain. Xumm allows for CORS
  calls to JWT endpoints.
---

# CORS (Browser)

CORS (Cross-Origin Resource Sharing) is a mechanism that allows a web page from one origin (domain) to access resources from another origin. In other words, it is a security feature implemented by web browsers that restricts a web page from making requests to a different domain than the one that served the web page.

The Xumm API endpoints **allow** **cross origin** requests: we want your web application to be able to make calls to the Xumm platform using the credential (JWT) you have received when a user logged in.&#x20;

If you are building a [backend-sdk-api.md](../backend-sdk-api.md "mention")integration, CORS is irrelevant.

If you are building something in the browser (a web application), the most convenient way to interact with the Xumm platform is through the Javascript/TypeScript SDK: [Broken link](broken-reference "mention").

{% hint style="info" %}
If you are using the Javascript/TypeScript SDK ([Broken link](broken-reference "mention")) the SDK will automatically make sure you are calling the right CORS enabled endpoints when a user signed in through the SDK.
{% endhint %}

If you are building your own, custom implementation, you will have to make sure you are calling the [**JWT routes**](https://xumm.readme.io/reference/ping-jwt): only our JWT (JSON Web Token) routes allow for cross origin calls, and serve the right headers to allow your browser to do so.
