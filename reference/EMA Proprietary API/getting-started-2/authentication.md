---
title: Authentication (Deprecated)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
ModMed's API uses the [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) standard for authorizing API calls. To authenticate requests, an access token must be included with each API request. This token identifies your application and defines which resources (e.g., Appointments, Patients) it can access. If your application has received explicit authorization from multiple practices, you can interact with the MMI FHIR API on behalf of each.

### Obtaining Authorization

OAuth 2.0 offers various grant types (or "methods") for acquiring an access token. Currently, the password grant flow is supported. To obtain a token, your application must send a POST request to the appropriate authentication endpoint.

### Authentication Endpoints

**Generic Sandboxes:**\
[https://stage.ema-api.com/ema-dev/firm/\{firm\_url\_prefix}/ema/ws/oauth2/grant](https://stage.ema-api.com/ema-dev/firm/\{firm_url_prefix}/ema/ws/oauth2/grant)

**Practice Sandboxes:**\
[https://stage.ema-api.com/ema-training/firm/\{firm\_url\_prefix}/ema/ws/oauth2/grant](https://stage.ema-api.com/ema-training/firm/\{firm_url_prefix}/ema/ws/oauth2/grant)

**Production:**\
[https://mmapi.ema-api.com/ema-prod/firm/\{firm\_url\_prefix}/ema/ws/oauth2/grant](https://mmapi.ema-api.com/ema-prod/firm/\{firm_url_prefix}/ema/ws/oauth2/grant)

### Request Parameters (Body , x-www-form-urlencoded)

grant\_type: password\
username: \{the username provided}
password: \{the password provided}

**NOTE:** Use [Authentication Endpoint](https://portal.api.modmed.com/reference/post_ws-oauth2-grant#/) for getting token for this portal.

**Example:**

```Text http
curl --location 'https://stage.ema-api.com/ema-dev/firm/apiportal/ema/ws/oauth2/grant' \
--header 'x-api-key: Zt9tXPIgz17uxEU6gkZPWa3ZAFhZOqm04oEDHC1f' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username=fhir_QfLlo' \
--data-urlencode 'password=925X3LZ505'
```

![](https://files.readme.io/0986c46764cf83e68c224c7753982048268f63afa8b86e09f3802b26bf4d2ef5-image.png)

Once you make the POST, you should get both the Access token and the Refresh tokens returned to you similar to the example here (the values are intentionally obfuscated):\
Sample Return:

```
{
"scope": "emapmsandbox01",
"token_type": "Bearer",
"access_token":
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJmaGlyX2lEdm1aIiwidXJsUHJlZml4IjoiZGVybXBtc2FuZGJveDQ5IiwidmVuZ
G9yIjoiZmhpcl9p…..",
"refresh_token":
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJmaGlyX2lEdm1aIiwidXJsUHJlZml4IjoiZGVybXBtc2FuZGJveDQ5IiwiaXNzIjo
ibW9kbWVkIiwidG9rZW5……..."
}
```

Once you have the Access Token, you will use that in each of the calls to the API. You can use the Refresh Token to obtain additional Access Tokens:\
**Example:**

```Text http
curl -X POST \
https://stage.ema-api.com/ema-dev/firm/emapmsandbox01/ema/ws/oauth2/grant \
-H 'Content-Type: application/x-www-form-urlencoded' \
-H 'Postman-Token: 7c553cdc-78bd-4548-b221-f2b32dd50c82' \
-H 'cache-control: no-cache' \
-H 'x-api-key: 5ca254dcc3hhftsy65sgsgsg6shhhh78njjjjjjjdshdshhsh' \
-d
'grant_type=refresh_token&refresh_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJmaGlyX2lEdm1aIiwidXJsUHJlZml
4IjoiZGVybXBtc2FuZGJveDQ5IiwiaXNzIjoibW9kbWVk……………………………….OSC9NtWqqwAMzSlI'
```

At which point, you will get back something like:

```
{
"scope": "emapmsandbox01",
"token_type": "Bearer",
"access_token":
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJmaGlyX2lEdm1aIiwidXJsUHJlZml4IjoiZGVybXBtc2FuZGJveDQ5IiwidmVuZ
G9yIjoiZmhpcl9pRHZtWkBkZXJtcG1zYW5kYm94NDkiLCJpc3MiOiJtb2RtZWQiLCJ0b2tlblR5cGUiOiJhY2Nlc3MiLCJwb2wiOiJjaGF
uZ2VtZSIsImp0aSI6ImQ5NDc4ND………….",
"refresh_token":
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJmaGlyX2lEdm1aIiwidXJsUHJlZml4IjoiZGVybXBtc2FuZGJveDQ5IiwiaXNzIjo
ibW9kbWVkIiwidG9rZW5UeXBlIjoicmV………………………...MzSlI"
}
```

**Note:** The refresh token will remain the same as what you sent in your POST.

Once you have the Access Token, you will use that in each of the calls to the API. For example, if you were making a GET call for a Patient, it would look something like this:

```Text http
curl -X GET \
https://stage.ema-api.com/ema-dev/firm/emapmsandbox01/ema/fhir/v2/Patient \
-H 'Authorization: Bearer
eyJ0eXAiOiJKV1QiLCJh……………………..GQ1Nzk2NTRjNGViOWJhYTdkZjY2NjBkNjdiIn0.WcuidhExBqQu7zlX1cQhD12JicoVpD
HouU_bvV_qWvA' \
-H 'Postman-Token: ce2d75cb-48f2-431f-b70e-007ceff4ad1e' \
-H 'cache-control: no-cache' \
-H 'x-api-key: 5ca254dcc3ee6372d2519htsg56hst7788hhstsfaghhdggg5'
```