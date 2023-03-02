# Xumm.user { ... }

xApp & Browser, unified user information

* `account` (r-address)
* `picture` (URL)
* `name`
* `domain`
* `source`
* `networkType`
* `networkEndpoint`
* `blocked`
* `kycApproved`
* `proSubscription`
* `profile`
* `token`, in case of xApp & Browser ("Web3"). SDK will take care of using @ created payloads from xApp / Browser, but in case a backend job wants to send: you can get the token here.  (`user_token` for payload GET @ Backend)
