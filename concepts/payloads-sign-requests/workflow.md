---
description: >-
  Xumm's workflow is designed to streamline the process of transaction signing
  and interaction with the XRP Ledger.
---

# Workflow

**Here's a step-by-step guide to understanding and implementing Xumm's workflow in your application:**

1. **Create a Payload**: Start by using Xumm's API to create a payload. A payload is essentially a transaction template containing all the details for the transaction you want the User to sign.
2. **Deliver the Payload to the User**: Once the payload is created, you need to deliver it to the User for signing. Xumm offers multiple delivery options, including push notifications, QR codes, and deep links. Choose the method that best suits your application.
3. **User Interaction**: The User will interact with the payload through the Xumm app. They have the option to either sign or reject the transaction.
4. **Retrieve the Result**: After the User has interacted with the payload, your application needs to retrieve the result [status-updates](status-updates/ "mention"). This can be done by fetching the result from Xumm's API. The result will indicate whether the User signed or rejected the transaction.
5. **Interact with the XRP Ledger**: If the User signed the transaction, your application can now interact with the XRP Ledger to finalize the transaction. This involves submitting the signed transaction to the XRP Ledger and handling any responses or confirmations.
6. **Provide Feedback to the User**: Finally, provide appropriate Feedback based on the transaction's outcome. This could be a confirmation message for a successful transaction or an error message if something went wrong.

**By following these steps, you can effectively integrate Xumm's workflow into your application and leverage its features for secure and streamlined transactions on the XRP Ledger.**
