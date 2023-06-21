---
description: >-
  CORS restricts access to resources on different domains to ensure privacy and
  security, allowing website owners to control access. As xApps run inside Xumm,
  allowing CORS is required for xApps.
---

# CORS (xApp)

## Troubleshooting&#x20;

If an xApp integration doesn't allow for running commands, and the console shows messages like "Couldn't connect to host", problems are a result of the same cause: CORS issues.

* The SDK can't reach Xumm (the app), so:
* "Could not contact Xumm host" error appears, and:
* For example: the `openSignRequest` trigger doesn't fire, the Sign Request doesn't open, and:
* Xumm keeps on trying, and is stalling the init. To see if the host can be reached - yielding "Attempt n » Retry" console messages (just to make sure it isn't a timing issue).

#### Find the cause

Check the following things:

1. Are you getting this messages from your frontend console, or backend (node?)
2. Do you have CORS setup correctly? (Allow iframe loading, allow CORS (origin: `*`)
3. Does your app run over http (instead of https with a valid certificate?)
4. Does your app run over https on a non standard (non TCP 443) port?
5. Some web server configurations don't allow CORS to work on a subdomain. Try running on a FQDN

While #3 and #4 should be valid, we've seen some Android phones where this prevented the integration from working. We use `ngrok` to work around the local http and non standard port development issues.





\
