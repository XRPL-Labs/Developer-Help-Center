---
description: >-
  Events fired by the SDK per environment. For the order of events, see the
  section per environment after the table with events.
---

# Xumm.on(event, fn)

|                                                Event | Environment          | Meaning                                                                                                                                                                                                   |
| ---------------------------------------------------: | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     <mark style="color:blue;">**`retrieved`**</mark> | xApp, Web3 (browser) | A valid signed in Xumm SDK session has been retrieved.                                                                                                                                                    |
|       <mark style="color:blue;">**`success`**</mark> | xApp, Web3 (browser) | A user is succesfully identified and signed in                                                                                                                                                            |
|         <mark style="color:blue;">**`ready`**</mark> | xApp, Web3 (browser) | The SDK is ready (final state) so your application can render                                                                                                                                             |
|  <mark style="color:purple;">**`retrieving`**</mark> | Web3 (browser)       | The SDK is trying to retrieve & verify an existing session                                                                                                                                                |
|      <mark style="color:purple;">**`logout`**</mark> | Web3 (browser)       | The SDK is going to destroy a pending signed in session                                                                                                                                                   |
|   <mark style="color:purple;">**`loggedout`**</mark> | Web3 (browser)       | The SDK destroyed a signed in session, a user can login again.                                                                                                                                            |
|       <mark style="color:purple;">**`error`**</mark> | Web3 (browser)       | An error occurred, see the browser console for more information                                                                                                                                           |
|          <mark style="color:orange;">**`qr`**</mark> | xApp (user event)    | <p>The QR code scan dialog in Xumm has been closed (dismissed or a QR code has been scanned)<br>From: <a data-mention href="xumm.xapp-.../scanqr.md">scanqr.md</a></p>                                    |
|     <mark style="color:orange;">**`payload`**</mark> | xApp (user event)    | <p>A Sign Request (payload) has been resolved (cancelled / signed / ...)<br>From: <a data-mention href="xumm.xapp-.../opensignrequest-....md">opensignrequest-....md</a></p>                              |
| <mark style="color:orange;">**`destination`**</mark> | xApp (user event)    | <p>The "Destination Picker" dialog in Xumm has been closed (dismissed or a destination has been selected)<br>From: <a data-mention href="xumm.xapp-.../selectdestination.md">selectdestination.md</a></p> |

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
