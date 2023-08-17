---
description: >-
  When building xApps, there are some tools to make building & sharing your xApp
  easier.
---

# Develop & Test

While developing your xApp, you may want to easily test & debug your web application. You may even benefit from live reaload during development. You can expose your local development environment with a tool like [https://ngrok.io](https://ngrok.io/) or [https://localtunnel.me](https://localtunnel.me/) and configure your public URL as your xApp URL.

You can get access to the remote browser console using the techniques explained in the [debugging.md](debugging.md "mention") article.

If you want to share your xApp with a small group of testers or team members, you can ask them for their Xumm Device Identifier (Xumm - Settings - Advanced). You can add up to 10 Device Identifiers as xApp testers, so they can open your sandboxed xApp.

{% hint style="info" %}
Warning! If you have multiple xApps (e.g. a live version & a test version, pointing to your development URL) please make sure to use the right API Key, otherwise your app can't communicate with the Xumm backend. Also note things like [xumm.userstore](../../js-ts-sdk/sdk-syntax/xumm.userstore/ "mention") are API Key & user bound.
{% endhint %}

When you want to develop in your local browser instead of in Xumm, please see the "**OTT Replay**" section in the [debugging.md](debugging.md "mention") article.

{% hint style="success" %}
We are currently working on a Desktop **xApp Development Application** so you can develop & test locally :tada: (Work in progress, more good things are coming)
{% endhint %}
