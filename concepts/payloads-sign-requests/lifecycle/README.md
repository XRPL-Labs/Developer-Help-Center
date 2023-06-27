---
description: >-
  Xumm's transaction lifecycle is a sequence of steps that ensures secure and
  efficient transaction processing on the XRP Ledger.
---

# Lifecycle

**Here's a comprehensive guide to understanding and implementing Xumm's transaction lifecycle:**

## 1. Transaction Template

Start by composing the transaction you want to be signed in JSON format, as per the [XRPL transaction format specification at xrpl.org](https://xrpl.org/transaction-types.html). You can include all [common fields](https://xrpl.org/transaction-common-fields.html) except "Account" and "Sequence", which will be automatically filled by Xumm.

Therefore, any JSON value you'd use to sign and send to an XRPL node can be sent to the Xumm SDK/API, with the (signing) account fields being added/filled being the only major difference.

All fields and values in the JSON transaction template sent to the Xumm SDK/API are passed on as-is, except for the following:

1. `Account`: If this field is part of the transaction template, it will be completely ignored, as the `Account` will be automatically filled based on the account the end user uses to sign the transaction with in the Xumm app.
2. `Sequence`: Based on the account used to sign by the end user in the Xumm app, the `Sequence` will be automatically filled by Xumm.
3. `LastLedgerSequence`: If a valid ledger index is entered in the `LastLedgerSequence` field, it will be passed on unchanged to the Xumm app. <mark style="color:orange;">However, if a</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**value <**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**`32570`**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**is entered**</mark><mark style="color:orange;">, the Xumm app will automatically calculate the</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**`{current ledger index}`**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">**+ the given amount of ledgers**</mark>, where `{current ledger index}` is based on the most recent closed ledger index at the moment the end user taps the button to accept & sign the sign request.

## 2. Payload Options

Configure Payload Options: Configure the payload options to customize the transaction request. Refer to the [Payload Options Documentation](https://xumm.readme.io/reference) for detailed information on the available options.&#x20;

## 3. User Token (Optional)

If you are using a backend flow, you can optionally include a user token. This token is specific to the user and can be used for personalized transactions.

## 4. Submit the Payload

Submit the payload to Xumm through the Xumm SDK or API. You can also use alternative language SDKs for this step. This initiates the transaction signing process.

## 5. Handle Client Interaction

The client, a mobile app, xApp, or desktop application, will interact with the payload. Implement logic to handle this interaction and guide the user through the signing process.

## 6. Resolve the Transaction

The user will either sign or reject the transaction. Your application should be ready to handle both outcomes and take appropriate action.

## 7. Retrieve Payload Results

After resolution, retrieve the payload results to understand the outcome of the transaction. You can use WebHooks, and WebSockets or verify through the SDK/API.

## 8. On-Ledger Verification

Finally, verify the transaction on the XRP Ledger. You can use libraries like [xrpl-client](https://www.npmjs.com/package/xrpl-client) or [verify-xrpl-signature](https://www.npmjs.com/package/verify-xrpl-signature) for on-ledger verification. Ensure to check for delivered\_amount and other relevant fields.

**Understanding and implementing Xumm's transaction lifecycle is crucial for creating secure and efficient transactions on the XRP Ledger through the Xumm platform.**
