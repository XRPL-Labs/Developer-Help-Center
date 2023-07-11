---
description: >-
  Polling, or repeated API calls, is a common method to fetch updates. However,
  in Xumm, it's not the recommended approach due to rate limits.
---

# API Call (polling)

**Instead of polling, consider these efficient alternatives:**

* **Webhooks**: Once a payload is resolved, Xumm can send a WebHook to your platform, eliminating the need for constant polling. Learn more: [webhooks](webhooks/ "mention").
* **Websocket Subscription**: Use Websocket to receive live status updates. Learn more: [websocket.md](websocket.md "mention").

Excessive polling can lead to your application being temporarily rate limited, disrupting your service. If your application has been rate limited, you will receive a notification email later the same day on the e-mail address entered in the application details in the [Xumm Developer Console](https://apps.xumm.dev).
