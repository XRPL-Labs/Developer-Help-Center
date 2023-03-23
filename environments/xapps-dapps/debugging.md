---
description: 'Debugging your xApp is tricky: it runs on your phone. How to access the logs?'
---

# Debugging

Some things that may help debugging your xApp:

## Remote JS Console

Using [https://remotejs.com](https://remotejs.com/) you can drop one line (script) in your page's `<head>` and get realtime access to the remote console (bi-directional).

## Replay OTT's

If you open your own xApp using the device you added in the Xumm Developer Console as debug device (using the Device Identifier), the OTT (one time token) can be replayed when visiting from the same IP address.

* Make sure your device (Xumm - Settings - Advanced) is whitelisted as Debug Identifier in the Xumm Developer Console
* Make sure your phone and computer are visiting from the same public IP address (e.g. by having them both on the same WiFi and internet connection
* Obtain your OTT in the xApp: it's the value of the `xAppToken` query parameter. Your xApp is being called with `https://your-url/?xAppToken=...`
* Now open your public xApp URL with `/force` appended, and include the xApp Token. E.g. if your xApp launch URL is:\
  `https://xumm.app/detect/xapp:sandbox.abcd1234`\
  ... You open (in your browser):\
  `https://xumm.app/detect/xapp:sandbox.abcd1234/force?xAppToken=...`

You will now see your xApp in your browser.

## Use your local dev URL as xApp URL

Use a tool like `ngrok` ([https://ngrok.io](https://ngrok.io/)) or `localtunnel.me` ([https://localtunnel.me](https://localtunnel.me/)) to temporarily publish your local development URL to a publicly available URL you can use to access your xApp during live debug/development.
