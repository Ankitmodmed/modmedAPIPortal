---
title: Authentication
deprecated: false
hidden: false
metadata:
  robots: index
---
ModMed's API uses the [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) standard for authorizing API calls. To authenticate requests, an access token must be included with each API request. This token identifies your application and defines which resources (e.g., Appointments, Patients) it can access. If your application has received explicit authorization from multiple practices, you can interact with the MMI FHIR API on behalf of each.

### Obtaining Authorization

OAuth 2.0 offers various grant types (or "methods") for acquiring an access token. 

This API utilizes the ‘client-credentials’ authorization flow.

### Authentication Endpoints

The endpoints to obtain a token are as follows:

**Staging/Development**
[https://ssoqa01-lb-01.m2qa.com/auth/realms/ema-fhir/protocol/openid-connect/token](https://ssoqa01-lb-01.m2qa.com/auth/realms/ema-fhir/protocol/openid-connect/token)

**Production**
[https://sso.ema.md/auth/realms/ema-fhir/protocol/openid-connect/token](https://sso.ema.md/auth/realms/ema-fhir/protocol/openid-connect/token)

<br />

### Request Parameters (Body , x-www-form-urlencoded)

grant_type: client_credentials  
client_id: \{the client_id provided}
client_secret: \{the secret provided}

**Example:**

```Text http
curl --location 'https://ssoqa01-lb-01.m2qa.com/auth/realms/ema-fhir/protocol/openid-connect/token' \
--header 'x-api-key: Zt9tXPIgz17uxEU6gkZPWa3ZAFhZOqm04oEDHC1f' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=' \
--data-urlencode 'client_secret='
```

Once you make the POST, you should get an Access token returned to you - similar to the example here (some values are intentionally obfuscated):  
Sample Return:

```
{
    "access_token": "eyJhbGciOiJSUzI1...........................9tL2F1dGgvcmVhbG1zL2VtYS1maGlyIiwic3ViIjoiODAzNTM2MTAtZmQ1NC00OTQTb_XHDm1qH6wxh5q3Y3mM4OqpiGoSNvFkog599C5n1EJqkmVdSig",
    "expires_in": 900,
    "refresh_expires_in": 0,
    "token_type": "Bearer",
    "not-before-policy": 0,
    "scope": "acl/enc_s acl/pat_s_name_dob_gen acl/prac_role_r acl/tsk_pmrecall_s acl/doc_ref_r acl/algy_intol_c acl/serv_req_r acl/insr_plan_r acl/org_s acl/slot_s acl/prac_s acl/diag_rprt_s acl/doc_ref_c acl/cond_s acl/acc_s acl/req_grp_s acl/trans_bndl_post acl/tsk_s acl/pat_s acl/pat_u acl/org_pay_s acl/algy_intol_s acl/loc_r acl/appmt_u acl/pat_r acl/obsv_ef_s acl/comp_c acl/fmly_his_ef_c acl/obsv_ef_r acl/cond_c acl/req_grp_r acl/chrg_item_c acl/appmt_c acl/pat_s_id acl/pmc_ocu_ef_s acl/proc_ef_s acl/tsk_r acl/val_set_r acl/fmly_his_s acl/org_r acl/enc_r acl/tsk_pmrecall_r acl/diag_rprt_r acl/serv_req_s acl/med_state_c acl/prac_c acl/cov_r acl/cov_s acl/chrg_item_s acl/bnry_c_url acl/doc_ref_s acl/med_state_r acl/algy_intol_r acl/fmly_his_r acl/chrg_item_r acl/cond_r acl/appmt_s acl/loc_s acl/appmt_r acl/prac_r acl/insr_plan_s acl/org_c acl/trans_bndl_diag_rprt_labs acl/org_pay_r acl/rel_person_r acl/trans_bndl_diag_rprt_urin acl/med_state_s acl/pat_c acl/pmc_ocu_ef_r acl/prac_role_s acl/proc_ef_r"
}
```


**Example:**

Once you have the Access Token, you will use that in each of the calls to the API. For example, if you were making a GET call for a Patient, it would look something like this:

```Text http
curl -X GET \
https://stage.ema-api.com/ema-dev/firm/emapmsandbox01/ema/fhir/v2/Patient \
-H 'Authorization: Bearer
eyJ0eXAiOiJKV1QiLCJh……………………..GQ1Nzk2NTRjNGViOWJhYTdkZjY2NjBkNjdiIn0.WcuidhExBqQu7zlX1cQhD12JicoVpD
HouU_bvV_qWvA' \
-H 'cache-control: no-cache' \
-H 'x-api-key: Zt9tXPIgz17uxEU6gkZPWa3ZAFhZOqm04oEDHC1f'
```
