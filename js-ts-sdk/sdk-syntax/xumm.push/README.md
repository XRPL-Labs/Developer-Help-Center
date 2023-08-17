# Xumm.push { ... }

When building an xApp, there are a couple of extra methods available. These endpoints only work for xApp enabled API credentials, and can be used to e.g. push notifications and context to XUMM, opening your xApp.

Because xApps are user related, they must always be supplied a `user_token`, or be called from JWT context. Alternatively, if granted extra permissions, a push destination can also be: `user_uuid` / `user_account`.
