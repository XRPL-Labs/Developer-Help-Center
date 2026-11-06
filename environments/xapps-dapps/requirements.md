---
description: Technical requirements for building an xApp
---

# Requirements

xApps are web apps, embedded in Xaman. They add value for users, using sign requests and their own interface to help users do things on the XRP Ledger and beyond. To build one, you need experience with frontend web development.

{% hint style="info" %}
**This page covers the technical requirements for building an xApp.** For the full review process, including what we require, how to request a review, and what happens after approval, see [xApp publishing and review](https://docs.xaman.dev/environments/xapps-dapps/xapp-publishing-and-review).&#x20;
{% endhint %}

### At a glance

1. Build your xApp. You can start with a sandboxed xApp right away.
2. Test it with up to 10 testers.
3. Meet the requirements on this page.
4. Submit your source code with a description of what your xApp does.
5. Our development team reviews the code and tests the xApp.
6. If approved, your xApp gets a public link that any Xaman user can open.

### Three types of xApp

| Type                    | Who can open it                      |
| ----------------------- | ------------------------------------ |
| Sandboxed               | You and up to 10 testers             |
| Link (QR/deeplink) only | Anyone you share the link or QR with |
| Public (listed)         | All Xaman users                      |

Each type has its own requirements further down this page.

### Key requirements

These are the requirements developers most often miss. The full list is in the [xApp publishing and review](https://docs.xaman.dev/environments/xapps-dapps/xapp-publishing-and-review) article.

* You've completed KYC, and you're not anonymous.
* The source code of your xApp, and of its backend if it has one, is public on GitHub. Listed xApps have two alternatives. See Public (listed) xApps.
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

* Simple accessible navigation
* Clear icons: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-b52a10d3e93d08b186523aad8c191160df521835%2Ficons.png?alt=media)
* Keep minimum content on screen, reduce clutter
* Use accessible fonts: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-193e315fb922fc30655a457360046b4da88a0965%2Ffonts.png?alt=media)
* Use a minimum of 16pt font for standard **body text**
* Test on different devices: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-56fa8d9839f6d5d4816430922d8ddf159a22e52d%2Fdevices.png?alt=media)
* Manage information on a logical level
* Consistency in design
* Use a 40x40px target area for touch controls
* Good (horizontal) alignment: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-08600bfcb154c195210b8c1c36312290689d5428%2Falignment.png?alt=media)
* Distinction between primary and secondary buttons: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-b3f2b36c8c90866250fcd941cfb6d9f35d0df88d%2Fbuttons.png?alt=media)
* Clear error text: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-2e6d9093e6ccd298442442d9b188d6e07d2ae1f3%2Ferror%20text.png?alt=media)
* Appropriate color contrast: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-4412ef0bbdd2b52ce75d25bb8c24761bbbfecd22%2Fcontrast.png?alt=media)
* Write in clear, plain English
* Human-like language: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-59c0f2773978c38c62d1f88605277215f348d810%2Fadd%20to%20cart.png?alt=media)
* Break up content into smaller parts: ![](https://416994804-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F61N8uUPfBBFEqPdV1U4Y%2Fuploads%2Fgit-blob-a48e340e577b5b2c830d699fc0d5cc98e76c6264%2Fcontent.png?alt=media)

**Accessibility tools:**

* Contrast checker 1: https://accessibleweb.com/color-contrast-checker
* Contrast checker 2: https://contrastchecker.com/
* Icon set: https://feathericons.com/

### Sandboxed xApps

* Full access, no restrictions.
* Only you and up to 10 testers can open it. You add testers by their Device ID in the Xaman Developer Console.
* Having a sandboxed xApp is not an endorsement. Do not present it as one, for example on social media.
* Building a sandboxed xApp does not guarantee that your xApp will be approved.

### Link (QR/deeplink) only xApps

* The xApp should look appealing.
* The xApp should respect different Xaman user screen sizes.
* The xApp should be well crafted: it should be clear what the xApp will do, and it should do what it promised to do.
* The xApp should have a clear support workflow, and it should offer terms and conditions and a privacy statement.

### Public (listed) xApps

* The xApp should add real Xaman wallet value. If there is no actual wallet or XRPL interaction where the integration adds value, it should be a website, not an xApp.
* Offer value (features people will appreciate or need) for a large part of the XRPL and Xaman user base.
* The frontend source code must either be open source, shared (under NDA) with XRPL Labs for review, or covered by a third-party security audit (code and dependencies, plus dependency update procedures) acceptable to XRPL Labs.
