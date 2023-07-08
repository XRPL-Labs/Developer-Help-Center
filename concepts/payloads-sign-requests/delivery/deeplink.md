---
description: >-
  Deep linking in Xumm enables developers to provide a seamless user experience
  by swiftly guiding users to interact with payloads.
---

# Deep Linking

### Benefits of Deep Linking:

* **When to Use**: Opt for deep linking when you want to minimize user steps and create a fluid transition between your app and Xumm.
* **Device Compatibility**: Deep linking works when the origin (your app or browser) and Xumm are on the same device (iOS/Android).
* **Link Creation**: Generate a deep link that opens Xumm with the payload ready for interaction, making interactions more seamless while keeping users engaged.
* **Return URL**: Set a return URL in the payload to redirect users back to your app or browser post-interaction, maintaining a smooth flow.

### Note for Web Origins:

For web origins, users return to the default browser, not necessarily the original tab. In order to make this smooth, handle session restoration to ensure continuity.

### User Perspective:

For end users, deep linking is a breeze. They tap a link, interact with the payload in Xumm, and return to your app effortlessly.
