---
title: Authentication
deprecated: false
hidden: false
metadata:
  robots: index
---
ModMed's API uses the [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) standard for authorizing API calls. To authenticate requests, an access token must be included with each API request. This token identifies your application and defines which resources (e.g., Appointments, Patients) it can access. If your application has received explicit authorization from multiple practices, you can interact with the MMI FHIR API on behalf of each.

### Obtaining Authorization

OAuth 2.0 offers various grant types (or "methods") for acquiring an access token. Currently, the password grant flow is supported. To obtain a token, your application must send a POST request to the appropriate authentication endpoint.

### Authentication Endpoints

[https://stage.ema-api.com/ema-qa/firm/8659/mmgi/ws/oauth2/grant](https://stage.ema-api.com/ema-qa/firm/8659/mmgi/ws/oauth2/grant)

### Request Parameters (Body , x-www-form-urlencoded)

grant\_type: password\
username: \{the username provided}
password: \{the password provided}

**NOTE:** Make sure to enable following settings:

1. Follow original HTTP Method: ON
2. Follow Authorization header: ON

**Example:**

```Text http
curl --location 'https://stage.ema-api.com/ema-qa/firm/8659/mmgi/ws/oauth2/grant' \
--header 'x-api-key: 5ca254dcc3ee6372d2513de176654321' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username=sample' \
--data-urlencode 'password=sample'
```

![](https://files.readme.io/240d033fadd6bc6d866508f9921af5fb371b2a8eb2ee482c07c56edd33e728e2-image.png)

Once you make the POST, you should get both the Access token returned to you similar to the example here (the values are intentionally obfuscated):\
Sample Return:

```text
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjlBMEMzQUQ3QzMzQTREQkFCM0Q2OUQzQjcxNDhGNTNDIiwidHlwIjoiYXQrand0In0.eyJpc3MiOiJodHRwczovL2lkcC5tb2RtZWRjbG91ZGRldi5jb206NTAwMSsIm5iZiI6MTczOTg3MTk3OCwiaWF0IjoxNzM5ODcxOTc4LCJleHAiOjE3Mzk4NzU1NzgsImF1ZCI6Imh0dHBzOi8vaWRwLm1vZG1lZGNsb3VkZGV2LmNvbTo1MDAxL3Jlc291cmNlcyIsInNjb3BlIjpbIkdyYW50VHlwZS5wYXNzd29yZCJdLCJjbGllbnRfaWQiOiJtbWdpY2xpZW50OTYiLCJjbGllbnRfT3JnSWQiOiI5NiIsImp0aSI6IjIzNzMwNjFGOTg1RUMxMzlCQzI0MTg0MDhCREMzRUQwIn0.cyh1xtYeXTYwDbm69lC1NO5Zd0PLDaGcrZplaAN3CWLQkz-6uyyDhpn_wG_6_YnxwvssoHfkY4yIe3q1Z0N80CQUuOJpJ82456HP1eFkU4gcv4K9f37XW_alAhbbjBqCOZhlTeHhzqlGVljJQt6iEWB0FecAgzXpQ2CNz2h6sbsQvm0WwvZ_Ed-0p8U1EcsJypZoEi1mOIcieaIuz9-WXUtB7vbtXFSOpnb-hYymaaozoekvc8g1GtdLKkTroWNO-iO0Tn8P3Cip84bQ1LGYVRki5WtO6Ve71aa0ymXaaXUx1JqzctCt85O_tp3MsxD72hsSRdo7BX5JBuJ-2bAI5A",
  "expires_in": 3600,
  "token_type": "Bearer",
  "scope": "GrantType.password"
}
```

Once you have the Access Token, you will use that in each of the calls to the API.\
Example:

```
curl --location 'https://stage.ema-api.com/ema-qa/firm/8659/mmgi/fhir/v2/ValueSet' \
--header 'x-api-key: 5ca254dcc3ee6372d2513de176654321' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IjlBMEMzQUQ3QzMzQTREQkFCM0Q2OUQzQjcxNDhGNTNDIiwidHlwIjoiYXQrand0In0.eyJpc3MiOiJodHRwczovL2lkcC5tb2RtZWRjbG91ZGRldi5jb206NTAwMSIsIm5iZiI6MTczOTg2NzUyNCwiaWF0IjoxNzM5ODY3NTI0LCJleHAiOjE3Mzk4NzExMjQsImF1ZCI6Imh0dHBzOi8vaWRwLm1vZG1lZGNsb3VkZGV2LmNvbTo1MDAxL3Jlc291cmNlcyIsInNjb3BlIjpbIkdyYW50VHlwZS5wYXNzd29yZCJdLCJjbGllbnRfaWQiOiJtbWdpY2xpZW50OTYiLCJjbGllbnRfT3JnSWQiOiI5NiIsImp0aSI6IjYxN0M3QzEwQzE3NjAzREU4MDEzNUU5OEFDQUUzMTQ4In0.F1iRq_JppRx0zrWlhoqEZ37Drd86Z3LhR1uPxoL2O5Ab4QHspAoUSX4RKfepAxdKWqr_RysZJpyXuOEoPznplzqiV5nn1taDb0dM9XdxyAH1O8xFFulH1z_H2fFWIbIwGO4zJF7256UQloAn3Y597eNWP857XG8JaEliQwbu9u59tYgpjxKe964XlfGYx0_pqBSarosSNU1DWVjOuIZiCX0_Ur2sbNob9edMwN8cM4z5PMASt71LIrJIB3kXKISeqtClo3xTsecX9e9rNpri-m8ACtk0iA-QSgGxc25Fz8vVA85FFmkECBgu-uRXgvj7P40k7asJGxWEZuGjhPXpHg'
```