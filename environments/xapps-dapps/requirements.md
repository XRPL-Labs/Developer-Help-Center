---
description: Technical requirements for building an xApp
---

# Requirements

xApps are web apps, embedded in Xaman. They add value for users, using sign requests and their own interface to help users do things on the XRP Ledger and beyond. To build one, you need experience with frontend web development.

{% hint style="info" %}
**This page covers the technical requirements for building an xApp.** For the full review process, including what we require, how to request a review, and what happens after approval, see [xApp publishing and review](xapp-publishing-and-review.md).
{% endhint %}

### At a glance

1. Build your xApp. You can start with a sandboxed xApp right away.
2. Test it with up to 10 testers.
3. Meet the requirements on this page and in [xApp publishing and review](xapp-publishing-and-review.md).
4. Request a review by creating a ticket in the [Xaman Support xApp](https://xaman.app/detect/xapp:xumm.support-md), with a link to your public source code and a description of what your xApp does.
5. Our team reviews your xApp in stages, including its code, functionality, and the project behind it.
6. If approved, your xApp gets a public link that any Xaman user can open.

### Three types of xApp

| Type                       | Who can open it                      |
| -------------------------- | ------------------------------------ |
| Sandboxed                  | You and up to 10 testers             |
| Approved (link or QR only) | Anyone you share the link or QR with |
| Listed                     | All Xaman users                      |

### Key requirements

These are the requirements developers most often miss. The full list is in the [xApp publishing and review](xapp-publishing-and-review.md) article.

* You've completed KYC, and you're not anonymous.
* The source code of your xApp, and of its backend if it has one, is public on GitHub.
* Your xApp never asks for an account secret or private keys, in any form.
* Your xApp never asks users to sign SetRegularKey or SignerListSet transactions. There are no exceptions.
* Use the user and account details from the xApp OTT. Do not build "Login with Xaman", "Connect Xaman", or "Disconnect Xaman" flows. See [Authorization & Credentials](https://docs.xaman.dev/concepts/authorization.md).
* Every change to your xApp, however small, needs a new review before it goes live.

### Technical

* Open external links in the OS browser, not inside Xaman. Use the [`openBrowser`](https://docs.xaman.dev/js-ts-sdk/sdk-syntax/xumm.xapp/openbrowser.md) call in the [Xaman UI interaction](https://docs.xaman.dev/environments/xapps-dapps/xumm-ui-interaction.md) layer. This stops users from navigating to another website by accident.
* For reliable user-bound storage, use the SDK [`userstore`](https://docs.xaman.dev/js-ts-sdk/sdk-syntax/xumm.userstore.md), not cookies or localStorage.
* Do not poll for payload status. Polling hits rate limits and is not the recommended approach. Use the [websocket we provide for status updates](https://docs.xaman.dev/concepts/payloads-sign-requests/status-updates/websocket.md), or the [`createAndSubscribe`](https://docs.xaman.dev/js-ts-sdk/sdk-syntax/xumm.payload/createandsubscribe.md) or [`subscribe`](https://docs.xaman.dev/js-ts-sdk/sdk-syntax/xumm.payload/subscribe.md) methods in the SDK. Backend applications can use a [webhook](https://docs.xaman.dev/concepts/payloads-sign-requests/status-updates/webhooks.md) instead. See [API Call (polling)](https://docs.xaman.dev/concepts/payloads-sign-requests/status-updates/api-call-polling.md) for why polling is discouraged.

### Styling

* Use your own colour scheme (independent of dark/light mode), or respect the [Xaman colour schemes](https://docs.xaman.dev/environments/xapps-dapps/style-guide.md). The user's styling is passed to your xApp in the `xAppStyle` query parameter.
* Set the background colour of your `<html>` and `<body>` tags to `transparent` from the first render. This prevents a white flash while your xApp loads, until styling has been applied.

### Accessibility

* Simple, accessible navigation
* Clear icons: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-b52a10d3e93d08b186523aad8c191160df521835%2Ficons.png?alt=media)
* Keep content on screen to a minimum, and reduce clutter
* Use accessible fonts: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-193e315fb922fc30655a457360046b4da88a0965%2Ffonts.png?alt=media)
* Use at least 16 px for standard **body text**
* Test on different devices, including a screen width of 360 px: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-56fa8d9839f6d5d4816430922d8ddf159a22e52d%2Fdevices.png?alt=media)
* Group related information together, in a logical order
* Keep your design consistent
* Use a touch area of at least 40 × 40 px for buttons and other touch controls
* Align elements consistently: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-08600bfcb154c195210b8c1c36312290689d5428%2Falignment.png?alt=media)
* Make primary and secondary buttons clearly different: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-b3f2b36c8c90866250fcd941cfb6d9f35d0df88d%2Fbuttons.png?alt=media)
* Clear error text: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-2e6d9093e6ccd298442442d9b188d6e07d2ae1f3%2Ferror%20text.png?alt=media)
* Appropriate colour contrast: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-4412ef0bbdd2b52ce75d25bb8c24761bbbfecd22%2Fcontrast.png?alt=media)
* Write in clear, plain English
* Use natural, human language: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-59c0f2773978c38c62d1f88605277215f348d810%2Fadd%20to%20cart.png?alt=media)
* Break up long content into smaller parts: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-a48e340e577b5b2c830d699fc0d5cc98e76c6264%2Fcontent.png?alt=media)

### Accessibility tools

* Contrast checker 1: [https://accessibleweb.com/color-contrast-checker](https://accessibleweb.com/color-contrast-checker)
* Contrast checker 2: [https://contrastchecker.com/](https://contrastchecker.com/)
* Icon set: [https://feathericons.com/](https://feathericons.com/)

### Sandboxed xApps

* Full access, no restrictions.
* Only you and up to 10 testers can open it. You add testers by their Device ID in the Xaman Developer Console.
* Having a sandboxed xApp is not an endorsement. Do not present it as one, for example on social media.
* Building a sandboxed xApp does not guarantee that your xApp will be approved.
