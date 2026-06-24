---
title: Authentication
hidden: false
---
The ModMed Certified FHIR API uses **OAuth 2.0** with the **SMART App Launch** framework to authorize requests. Your application obtains an access token, then includes it as a `Bearer` token on every FHIR call. Which flow you use depends on the kind of application you're building — see **App Types** below.

> 📘 Production only
>
> The Certified FHIR API does not have a public sandbox. Authorization and API calls run against the production environment.

## Endpoints

| Purpose           | URL                                                                                |
| :---------------- | :--------------------------------------------------------------------------------- |
| Authorization     | `https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/auth`                 |
| Token             | `https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token`                |
| FHIR base (`aud`) | `https://fhirmp.mmi.prod.fhir.ema-api.com/fhir/r4`                                 |
| Discovery         | `https://fhirmp.mmi.prod.fhir.ema-api.com/fhir/r4/.well-known/smart-configuration` |

Token endpoint authentication is `client_secret_post` — send your `client_id` and `client_secret` in the request body. PKCE (`S256`) is supported and recommended for user-facing apps.

## App Types

Before registering, decide what type of application you're building — it determines how users authenticate and which scopes you request.

- **Bulk FHIR (system / background)** — If you're working with a practice and need access to their providers' and patients' clinical data at the practice level, build a Bulk FHIR application. A practice Admin adds your `ClientId` to their practice once, and your application accesses data as needed using the `client_credentials` flow. No per-user authentication.
- **Patient apps** — Require a Patient at the practice (with valid Patient Portal username/password) to authenticate. After the first **Standalone** authentication, a link is placed inside the patient portal for repeated access and for the patient to manage or disable access.
- **Provider apps** — Require a Provider at the practice to authenticate with the same credentials they use for the EHR. After authenticating, a link is placed inside their EHR instance (location varies by scope) to launch your app from within the EHR.
- **Patient and Provider apps** — Handle authentication for both patients and providers.

For all Patient and Provider app types, the vendor must provide the initial **Standalone** authentication mechanism. Once a user authenticates via the Standalone flow, an in-context **EHR Launch** link is placed in their UI for ongoing use.

## Authorization flows

### Authorization Code (with PKCE) — Patient & Provider apps

1. Redirect the user's browser to the **authorization** endpoint with: `response_type=code`, `client_id`, `redirect_uri`, `scope` (space-separated), `state`, `aud` (the FHIR base URL above), and `code_challenge` + `code_challenge_method=S256`.
2. The user authenticates — Patient Portal credentials for patient apps, EHR credentials for provider apps. For **EHR Launch**, the app is started from within EMA and receives a `launch` parameter (include the `launch` scope).
3. The server redirects back to your `redirect_uri` with a `code` and your `state`.
4. Exchange the code at the **token** endpoint: `grant_type=authorization_code`, `code`, `redirect_uri`, `code_verifier`, `client_id`, `client_secret`.
5. You receive an `access_token` (plus an `id_token` when `openid` is requested, and a `refresh_token` when `online_access`/`offline_access` is granted). Send the access token as `Authorization: Bearer <token>` on FHIR calls.

### Client Credentials — Bulk FHIR / background apps

POST to the **token** endpoint with `grant_type=client_credentials`, `client_id`, and `client_secret`. No user interaction is involved. Use the returned `access_token` as a `Bearer` token.

## Scopes

Request only the scopes your application needs. Scopes fall into four groups.

**Context scopes** — control what gets put in the token

| Scope            | Standalone              | EHR Launch                      | What it does                                        |
| :--------------- | :---------------------- | :------------------------------ | :-------------------------------------------------- |
| launch/patient   | Triggers patient picker | Passes patient from EHR context | Puts patient claim in the token                     |
| launch/encounter | Rarely useful           | Passes encounter from EHR       | Puts encounter claim in token                       |
| launch           | Never                   | Always required                 | Tells auth server to honor the EHR's launch context |

**Identity scopes** — control what you know about the logged-in user

| Scope    | When to use                                          | What it does                                                       |
| :------- | :--------------------------------------------------- | :----------------------------------------------------------------- |
| openid   | Always                                               | Required for OIDC — enables id\_token                              |
| profile  | When you need user name/email                        | Adds basic profile claims to id\_token                             |
| fhirUser | When you need to look up the user as a FHIR resource | Adds a fhirUser claim — a URL like Practitioner/abc123 you can GET |

**Session scopes** — control token lifetime

| Scope           | When to use                  | What it does                                                |
| :-------------- | :--------------------------- | :---------------------------------------------------------- |
| online\_access  | Most apps                    | Refresh token that expires when the user's EMA session ends |
| offline\_access | Background/long-running apps | Refresh token that doesn't expire with the session          |

**Resource scopes** — control what FHIR data you can read

| Scope               | When to use           | What it does                                                                                  |
| :------------------ | :-------------------- | :-------------------------------------------------------------------------------------------- |
| patient/Resource.rs | Patient context apps  | Read/search that resource scoped to the token's patient — can't read other patients' data     |
| user/Resource.rs    | Provider context apps | Read/search that resource as the logged-in user — broader access across patients they can see |

### Recommended scopes by app type

| App Type                        | Required                                         | Makes sense                                      | Doesn't make sense                   |
| :------------------------------ | :----------------------------------------------- | :----------------------------------------------- | :----------------------------------- |
| Standalone (patient picker)     | openid, launch/patient                           | fhirUser, online\_access, patient/\*.rs          | launch, launch/encounter, user/\*.rs |
| EHR Launch — Patient            | openid, launch, launch/patient                   | fhirUser, online\_access, patient/\*.rs          | launch/encounter, user/\*.rs         |
| EHR Launch — Provider           | openid, launch, launch/encounter                 | fhirUser, online\_access, user/\*.rs             | launch/patient, patient/\*.rs        |
| EHR Launch — Patient + Provider | openid, launch, launch/patient, launch/encounter | fhirUser, online\_access, patient/_.rs,user/_.rs | —                                    |
| Background / automated          | openid, offline\_access                          | user/\*.rs                                       | launch/patient, launch/encounter     |

## Register

Haven't registered yet? See [Become a ModMed Certified FHIR API Vendor](doc:register-to-become-a-modmed-certified-fhir-api-vendor) to choose your app type and configure your application.
