# Xumm.ping()

Can be used to check connectivity / JWT (credential) validity & to obtain basic information about the calling credentials.

#### Sample response

```json
{
  "pong": true,
  "auth": {
    "quota": {},
    "application": {
      "uuidv4": "8525e32b-1bd0-4839-af2f-f794874a80b0",
      "name": "Some App",
      "webhookurl": "https://webhook.site/3e5dee90-a654-4e34-8112-c4391247a8ee",
      "disabled": 0
    },
    "call": {
      "uuidv4": "4b97cf7a-1837-471f-baed-2ebebcf5adb4"
    }
  }
}
```
