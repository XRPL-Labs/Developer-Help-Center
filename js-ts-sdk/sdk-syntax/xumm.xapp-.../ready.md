---
description: >-
  When using the native Xumm loader screen for your xApp (until your xApp is
  ready, fully hydrated, booted, etc.) you call this method to remove the Xumm
  loading screen.
---

# ready()

To prevent showing a double loader (first the Xumm xApp loader, then your xApp's loader while hydrating / booting) you can enable the "**Xumm Loader Screen**" option in the Xumm Developer Console (xApp tab). The xApp will then show the Xumm native loader, until your application calls the `ready()` method on the Xumm SDK.

### Syntax

```javascript
// First your app loads, fetches,etc.
// Then you have all the information you need to
// render & show your app, and you call:

xumm.xapp.ready()
```

#### Exception flows

1. **The xApp doesn't load, to be able to debug the app needs to be displayed (e.g. reverse proxy 502 error or some other app error, preventing the SDK's `ready()` call being made).**\
   ****With Xumm in Developer Mode, the Xumm loading screen shows a 'Proceed to xApp' button at the Xumm loader screen, below the spinner. This way you can dismiss the Xumm loader and view the underlying problem.
2. **The xApp takes very long to load or doesn't load at all: users are confronted with a long wait.**\
   If the `ready()` method in the Xumm SDK isn't called within \~6 seconds a label + button is made visible: "xApp is slow to respond..." `[Contact Developer]`.\
   This button then opens the Support URL for the xApp as entered in the Developer Console. For&#x20;
