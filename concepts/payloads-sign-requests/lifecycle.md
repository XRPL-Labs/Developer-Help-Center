# Lifecycle

## 1. Transaction Template

Compose the transaction you would like to sign in JSON format, as per the [XRPL transaction format specification at xrpl.org](https://xrpl.org/transaction-types.html). All [common fields](https://xrpl.org/transaction-common-fields.html) can also be part of your transaction template.

Therefore, any JSON value you'd use to sign and send to an XRPL node can be sent to the Xumm SDK/API, with the (signing) account fields being added/filled being the only major difference.

All fields and values in the JSON transaction template sent to the Xumm SDK/API are passed on as-is, except for:

1. `Account`: If this field is part of the transaction template, it will be completely ignored, as the `Account` will be automatically filled based on the account the end user uses to sign the transaction with in the Xumm app.
2. `Sequence`: Based on the account used to sign by the end user in the Xumm app, the `Sequence` will be automatically filled by Xumm.
3. `LastLedgerSequence`: If a valid ledger index is entered in the `LastLedgerSequence` field, it will be passed on unchanged to the Xumm app. <mark style="color:orange;">However, if a</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**value <**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`32570`**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**is entered**</mark><mark style="color:orange;">, the Xumm app will automatically calculate the</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**`{current ledger index}`**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**+ the given amount of ledgers**</mark>, where `{current ledger index}` is based on the most recent closed ledger index at the moment the end user taps the button to accept & sign the sign request.

## 2. Payload options

... [https://xumm.readme.io/reference](https://xumm.readme.io/reference)

## 3. User token (optional)

... (Only backend flow, Web3/App already specify)

## 4. Submit payload

... (Xumm SDK, alt. languages SDKs, API

## 5. Client interaction

...  (Mobile, xApp, Desktop, ...)

## 6. Resolve

... (User signs or rejects)

## 7. Payload results

... (WebHook, WebSocket, verify through SDK/API (!))

## 8. On ledger verification

... ([https://www.npmjs.com/package/xrpl-client](https://www.npmjs.com/package/xrpl-client), [https://www.npmjs.com/package/verify-xrpl-signature](https://www.npmjs.com/package/verify-xrpl-signature)), `delivered_amount`, ...
