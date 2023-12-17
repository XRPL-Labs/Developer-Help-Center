---
description: >-
  The Xumm API/SDK is designed to be network-independent, providing flexibility
  for developers and end users. This means that the end user determines the
  network on which transactions occur.
---

# Networks

However, a payload can include a forced network identifier to specify a particular network. When a user signs a payload, the result includes information about the network the user was on when signing, allowing developers to track and manage transactions across different networks.&#x20;

{% hint style="info" %}
If your payload contains a `NetworkID`, it is only valid for the given network. Xumm will ask a user to switch to the given network (starting Xumm 2.6.0)
{% endhint %}

### Key Points:

1. **Network Independence:** The Xumm API/SDK operates independently of the network, giving the end user the freedom to choose their preferred network in the Xumm app.
2. **Network Information in Results**: The results of a signed payload include information about the network the user was on at the time of signing.
3. **Forced Network Identifier**: A user can be on any network while signing. You must check for the expected result in the Payload results. Alternatively, you can include a forced network identifier in a payload to specify a particular network.
4. **Network Information in OTT Data**: xApp OTT data also includes network information, providing additional resources for developers to manage transactions.
5. **User Experience**: The choice of the network result in loss of goods or funds: imagine getting paid on Testnet, while delivering actual sold goods expecting a mainnet payment. It's important to consider this in your application development process.
