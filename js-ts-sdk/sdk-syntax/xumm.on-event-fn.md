---
description: >-
  Events fired by the SDK per environment. For the order of events, see the
  section per environment after the table with events.
---

# Xumm.on(event, fn)

<table><thead><tr><th width="202" align="right">Event</th><th width="218.33333333333331">Environment</th><th>Meaning</th></tr></thead><tbody><tr><td align="right"><mark style="color:blue;"><strong><code>retrieved</code></strong></mark></td><td>xApp, Web3 (browser)</td><td>A valid signed in Xumm SDK session has been retrieved.</td></tr><tr><td align="right"><mark style="color:blue;"><strong><code>success</code></strong></mark></td><td>xApp, Web3 (browser)</td><td>A user is succesfully identified and signed in</td></tr><tr><td align="right"><mark style="color:blue;"><strong><code>ready</code></strong></mark></td><td>xApp, Web3 (browser)</td><td>The SDK is ready (final state) so your application can render</td></tr><tr><td align="right"><mark style="color:purple;"><strong><code>retrieving</code></strong></mark></td><td>Web3 (browser)</td><td>The SDK is trying to retrieve &#x26; verify an existing session</td></tr><tr><td align="right"><mark style="color:purple;"><strong><code>logout</code></strong></mark></td><td>Web3 (browser)</td><td>The SDK is going to destroy a pending signed in session</td></tr><tr><td align="right"><mark style="color:purple;"><strong><code>loggedout</code></strong></mark></td><td>Web3 (browser)</td><td>The SDK destroyed a signed in session, a user can login again.</td></tr><tr><td align="right"><mark style="color:purple;"><strong><code>error</code></strong></mark></td><td>Web3 (browser)</td><td>An error occurred, see the browser console for more information</td></tr><tr><td align="right"><mark style="color:orange;"><strong><code>qr</code></strong></mark></td><td>xApp (user event)</td><td>The QR code scan dialog in Xumm has been closed (dismissed or a QR code has been scanned)<br>From: <a data-mention href="xumm.xapp/scanqr.md">scanqr.md</a></td></tr><tr><td align="right"><mark style="color:orange;"><strong><code>payload</code></strong></mark></td><td>xApp (user event)</td><td>A Sign Request (payload) has been resolved (cancelled / signed / ...)<br>From: <a data-mention href="xumm.xapp/opensignrequest.md">opensignrequest.md</a></td></tr><tr><td align="right"><mark style="color:orange;"><strong><code>destination</code></strong></mark></td><td>xApp (user event)</td><td>The "Destination Picker" dialog in Xumm has been closed (dismissed or a destination has been selected)<br>From: <a data-mention href="xumm.xapp/selectdestination.md">selectdestination.md</a></td></tr></tbody></table>

## Event order

The following order of events can be expected per environment.

{% hint style="info" %}
Note about the **`ready`** vs the **`success`** event:\
\
The **`ready`** event fires if the **SDK state** is ready for the rendering of your application. This **does not have to mean** the SDK is signed in: it just means the SDK is **ready**. \
\
If you want to know a user&#x20;
{% endhint %}

### xApp (always auto-signed in)

1. `retrieved` - xApps always auto-resolve
2. `success`- all information is populated to SDK properties (Promises)&#x20;
3. `ready` - ready to render your application with the correct Xumm SDK state

### Web3 (browser) - Signed out & then signing in

1. `retrieving` - but the user is signed out
2. `ready` - ready to render your application with the correct Xumm SDK state, but the user **must still** log in
3. _<mark style="background-color:yellow;">The user signs in</mark>_
4. `success` - all information is populated to SDK properties (Promises)&#x20;

### Web3 (browser) - Already signed in

1. `retrieving` - existing session information is being fetched & verified
2. `success` - all information is populated to SDK properties (Promises)&#x20;
3. `retrieved` - you are dealing with an already signed in user
4. `ready` - ready to render your application with the correct Xumm SDK state
