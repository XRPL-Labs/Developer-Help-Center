---
description: >-
  With xAppBuilder, you can now conveniently connect your localhost for an
  efficient and real-time development experience. This video provides an
  overview of connecting your localhost.
---

# Connecting localhost to xAppBuilder

{% embed url="https://www.youtube.com/watch?v=F0giTJuzYvI" %}

**Step 1: Create Your xApp**

Begin by opening your preferred code editor (in this case, we are using VS Code). Establish a project folder, and within this, create an index.html file. Type some text between the body tag.

Next, install the Live Server extension for VS Code.

Then, initiate the Live Server by clicking the 'Go Live' button/link located in the bottom right corner of VS Code. Take note of the port number that is displayed.

**Step 2: Make Your Website or Web Service Globally Accessible**

In your terminal, execute the command npm install -g localtunnel. If you encounter a permission error, use sudo npm install -g localtunnel.

Following this, run `lt --port 5500`, making sure to replace '5500' with the port number noted in Step 1.

The terminal will output a unique URL. Copy this, and open it in your browser. Here, submit your IP address (if you are unsure of your IP, a quick Google search of 'whatsmyip' will provide it).

For further information about this package, you can refer to the official [Localtunnel documentation](https://theboroer.github.io/localtunnel-www/).

**Step 3: Set Up Your Xumm Developer Console Account**

Navigate to the [Xumm Developer Console](https://apps.xumm.dev/) and create an xApp account.

Paste the URL acquired in Step 2 into the 'WebApp URL' section. In the 'Debug Device ID' section, enter your device ID (which can be found by navigating through Xumm -> settings -> advanced -> Device ID).

**Step 4: Access Your xApp on xAppBuilder**

Open xAppBuilder and scan the provided QR code using Xumm. Afterward, click on the xApp within xAppBuilder.

Now, when you make and save changes to your code in the VS code editor, these changes will be reflected in xAppBuilder, allowing for real-time modifications and testing.
