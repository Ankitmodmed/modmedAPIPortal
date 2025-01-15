---
name: Authorization Flow
---
## How to create a token

**Sample Request for Token**

```Text bash
curl -X POST \
--location 'https://ssoqa01-lb-01.m2qa.com/auth/realms/ema-service-account/protocol/openid-connect/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<user>' \
--data-urlencode 'client_secret=<pass>'
```