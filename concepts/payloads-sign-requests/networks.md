---
description: >-
  The Xumm API/SDK is designed to be network-independent, providing flexibility
  for developers and end users. This means that the end user determines the
  network on which transactions occur.
---

# Networks

However, a payload can include a forced network identifier to specify a particular network. When a user signs a payload, the result includes information about the network the user was on when signing, allowing developers to track and manage transactions across different networks.&#x20;

### Key Points:

1. **Network Independence:** The Xumm API/SDK operates independently of the network, giving the end user the freedom to choose their preferred network.
2. **Forced Network Identifier**: Include a forced network identifier in a payload to specify a particular network.
3. **Network Information in Results**: The results of a signed payload include information about the network the user was on at the time of signing.
4. **Network Information in OTT Data**: xApp OTT data also includes network information, providing additional resources for developers to manage transactions.
5. **User Experience**: The choice of the network can impact the user experience and transaction processing times, so it's important to consider this in your application development process.
