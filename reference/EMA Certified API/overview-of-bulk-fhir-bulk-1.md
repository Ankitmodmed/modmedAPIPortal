---
title: Overview of Bulk FHIR Bulk
deprecated: false
hidden: false
metadata:
  robots: index
---
ModMed supports a Bulk FHIR API implementation so that authorized vendors can access data from practices in a bulk manner. This could be data for all patients in a practice; data for groups of patients in a practice or all data from a practice. The purpose of this could be for research or analyzing the population data to help practices serve their patients better.

The individual API calls would need a large number of calls to access the same amount of data that could be retrieved in a single bulk API call. Initially, the Bulk data client will kick off the request for data to the server. Once the request is made, a response will be returned which will allow the client to know how to get the status of the request. Bulk requests will take time depending on the amount of data being prepared for return.

The Bulk client will need to poll the status URL periodically to check on the status of the request. Once the bulk processing is done by the server, a manifest file will be created which will have all the ndjson files that have the FHIR bulk data.

**General Process**\
The general process for apps built upon the Certified FHIR API is as follows:

1. Register with MMI: [https://fhir-vendor-dashboard.kube.prod.mmicse.com/](https://fhir-vendor-dashboard.kube.prod.mmicse.com/)
2. Create a Bulk FHIR application:

   ![](https://files.readme.io/e1fb26b4a31e13b6752f427975aa5b61b4d62cbfd246c33a1215f9b7755b8331-image.png)
3. Your app will be created in a ‘Disabled’ state:

   ![](https://files.readme.io/6e0eec5f9f8729070c27ec7b70d4488e132e9a10437d5f18a2fe664f425fa388-image.png)
4. For Bulk applications, This type of app will require consent from the practice. A Practice can provide your app consent by adding your app’s ClientID to their ‘Manage Bulk FHIR’ section in their Admin section:

   ![](https://files.readme.io/f17458ce586ae36a96713a1e7ca6af387a3d56bd5e6dcbe250ca91aae3c36b98-image.png)
5. Once a customer has added you, your app will become ‘Enabled’:

   ![](https://files.readme.io/422bdbad072a8235be230e6c8b7c01c91b1ea04b85372eb0e0846d647c4d8518-image.png)

**Authentication**

The vendor needs to authenticate with something similar to the following.\
For assistance, [this](https://hl7.org/fhir/smart-app-launch/example-backend-services.html#step-3-access-token) has a good tutorial about how to connect.

POST: [https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token](https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token)

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>

      </th>

      <th style={{ textAlign: "left" }}>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        client\_id (here you would have your client ID but here is a sample one)
      </td>

      <td style={{ textAlign: "left" }}>
        fhir000623719917a5c0008fa3b07182314edeb0cfc804639cfa5e
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        scope
      </td>

      <td style={{ textAlign: "left" }}>
        system/AllergyIntolerance.rs\\
        system/CarePlan.rs
        system/CarePlan.rs
        system/CareTeam.rs
        system/DocumentReference.rs
        system/DiagnosticReport.rs
        system/Goal.rs system/Condition.rs
        system/Immunization.rs
        system/Observation.rs
        system/Medication.rs
        system/MedicationRequest.rs
        system/Patient.rs system/Procedure.rs
        system/Provenance.rs
        system/Device.rs system/Encounter.rs
        system/Organization.rs
        system/Practitioner.rs
        system/PractitionerRole.rs
        system/Location.rs
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        encryption\_method
      </td>

      <td style={{ textAlign: "left" }}>
        ES384
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        client\_assertion
      </td>

      <td style={{ textAlign: "left" }}>
        eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzM
        4NCIsImtpZCI6IjRiNDlhNzM5ZDFlYjEx
        NWIzMjI1ZjRjZjliZWI2ZDFiIn0.eyJpc3
        MiOiJmaGlyMDAwNjIzNzE5OTE3YTVj
        MDAwOGZhM2IwNzE4MjMxNGVkZWI
        wY2ZjODA0NjM5Y2ZhNWUiLCJzdWIi
        OiJmaGlyMDAwNjIzNzE5OTE3YTVjM
        DAwOGZhM2IwNzE4MjMxNGVkZWIw
        Y2ZjODA0NjM5Y2ZhNWUiL…dWQiOi
        JodHRwczovL3Nzby5lbWEubWQvYX
        V0aC9yZWFsbXMvZmhpci9wcm90b2
        NvbC9vcGVuaWQtY29ubmVjdC90b2tl
        biIsImV4cCI6MTY4MTI0MjgzNSwianR
        pIjoiZTkyYWNiNDk5NTFlNjdiMjRhYTlk
        MTYwNjM0YzU3ODlkYWNlMTgyMjAz
        Nzc0OTIxZmMxMzA3MDE3NjViZDc4
        NyJ9.KKnqeIWCpJ-OlfSqe--YPCzIlkQ
        6l8skQW\_9CEgsksprosJUfK7huxhagi
        NeuJX\_5fem\_OBfFW5mMmuD9sGXOSZ8cU-pk5vWmi2Osg3lOs2gqWFP6Olh0O68HLDQ4z
      </td>
    </tr>
  </tbody>
</Table>

```
curl --location
'https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/toke
n' \
--header 'client_assertion:
eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzM4NCIsImtpZCI6IjRiNDlhNzM5ZDFlYjExN
WIzMjI1ZjRjZjliZWI2ZDFiIn0.eyJpc3MiOiJmaGlyMDAwNjIzNzE5OTE3YTVjMD
AwOGZhM2IwNzE4MjMxNGVkZWIwY2ZjODA0NjM5Y2ZhNWUiLCJzdWIiOiJmaGlyMDA
wNjIzNzE5OTE3YTVjMDAwOGZhM2IwNzE4MjMxNGVkZWIwY2ZjODA0NjM5Y2ZhNWUi
LCJhdWQiOiJodHRwczovL3Nzby5lbWEubWQvYXV0aC9yZWFsbXMvZmhpci9wcm90b
2NvbC9vcGVua...4MTI0MjgzNSwianRpIjoiZTkyYWNiNDk5NTFlNjdiMjRhYTlkM
TYwNjM0YzU3ODlkYWNlMTgyMjAzNzc0OTIxZmMxMzA3MDE3NjViZDc4NyJ9.KKnqe
IWCpJ-OlfSqe--YPCzIlkQ6l8skQW_9CEgsksprosJUfK7huxhagiNeuJX_5fem_O
BfFW5mMmuD9sGX-OSZ8cU-pk5vWmi2Osg3lOs2gqWFP-6Olh0O68HLDQ4z&client
_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-ty
pe%3Ajwt-bearer&grant_type=client_credentials&scope=system%2FAlle
rgyIntolerance.rs%20system%2FCarePlan.rs%20system%2FCarePlan.rs%2
0system%2FCareTeam.rs%20system%2FDocumentReference.rs%20system%2F
DiagnosticReport.rs%20system%2FGoal.rs%20system%2FCondition.rs%20
system%2FImmunization.rs%20system%2FObservation.rs%20system%2FMed
ication.rs%20system%2FMedicationRequest.rs%20system%2FPatient.rs%
20system%2FProcedure.rs%20system%2FProvenance.rs%20system%2FDevic
e.rs%20system%2FEncounter.rs%20system%2FOrganization.rs%20system%
2FPractitioner.rs%20system%2FPractitionerRole.rs%20system%2FLocat
ion.rs' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie:
AWSALB=unoyjfhN+Xj8hm4ZvELsYGL4LaPYUMclDJ3GnN0jy+N7iwFWQNxXLkWDsP
clcbmicAvYjLXi8EdxCc+NT6qyyOu/O19OKy1LvESOTCpyp0DLHP2L+0tuagumn6p
T;
AWSALBCORS=unoyjfhN+Xj8hm4ZvELsYGL4LaPYUMclDJ3GnN0jy+N7iwFWQNxXLk
WDsPclcbmicAvYjLXi8EdxCc+NT6qyyOu/O19OKy1LvESOTCpyp0DLHP2L+0tuagu
mn6pT' \
--data-urlencode
'client_id=fhir000623719917a5c0008fa3b07182314edeb0cfc804639cfa5e
' \
--data-urlencode 'scope=system/AllergyIntolerance.rs
system/CarePlan.rs system/CarePlan.rs system/CareTeam.rs
system/DocumentReference.rs system/DiagnosticReport.rs
system/Goal.rs system/Condition.rs system/Immunization.rs
system/Observation.rs system/Medication.rs
system/MedicationRequest.rs system/Patient.rs system/Procedure.rs
system/Provenance.rs system/Device.rs system/Encounter.rs
system/Organization.rs system/Practitioner.rs
system/PractitionerRole.rs system/Location.rs' \
--data-urlencode 'encryption_method=ES384' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode
'client_assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzM4NCIsImtpZCI6IjR
iNDlhNzM5ZDFlYjExNWIzMjI1ZjRjZjliZWI2ZDFiIn0.eyJpc3MiOiJmaGlyMDAw
NjIzNzE5OTE3YTVjMDAwOGZhM2IwNzE4MjMxNGVkZWIwY2ZjODA0NjM5Y2ZhNWUiL
CJzdWIiOiJmaGlyMDAwNjIzNzE5OTE3YTVjMDAwOGZhM2IwNzE4MjMxNGVkZWIwY2
ZjODA0NjM5Y2ZhNWUiLCJhdWQiOiJodHRwczovL3Nzby5lbWEubWQvYXV0aC9yZWF
sbXMvZmhpci9wcm90b2NvbC9vcGVuaWQtY29ubmVjdC90b2tlbiIsImV4cCI6MTY4
MTI0MjgzNSwianRpIjoiZTkyYWNiNDk5NTFlNjdiMjRhYTlkMTYwNjM0YzU3ODlkY
WNlMTgyMjAzNzc0OTIxZmMxMzA3MDE3NjViZDc4NyJ9.KKnqeIWCpJ-OlfSqe--YP
CzIlkQ6l8skQW_9CEgsksprosJUfK7huxhagiNeuJX_5fem_OBfFW5mMmuD9sGX-O
SZ8cU-pk5vWmi2Osg3lOs2gqWFP-6Olh0O68HLDQ4z' \
--data-urlencode
'client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer'
{
"access_token":
"eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJzM3Rnbi0taFpz
MkNVaEF3anhiSUdSVWFWZG83ZFMyUlNIMXVLSW9Ua0lvIn0.eyJleHAiOjE2ODEyN
DQzMzUsImlhdCI6MTY4MTI0MjUzNSwianRpIjoiYWViODEyMjQtNWI5ZC00OTVmLW
IwMDUtMDgyMmE3YjJlMGU0IiwiaXNzIjoiaHR0cHM6Ly9zc28uZW1hLm1kL2F1dGg
vcmVhbG1zL2ZoaXIiLCJzdWIiOiI1MDI3MDIyYy0zMjQ5LTRlMTYtODg2Yy02MDQx
OTI3M2EyZjMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJmaGlyMDAwNjIzNzE5OTE3Y
TVjMDAwOGZhM2IwNzE4MjMxNGVkZWIwY2ZjODA0NjM5Y2ZhNWUiLCJzY29wZSI6Im
xhdW5jaCBzeXN0ZW0vRW5jb3VudGVyLnJzIHN5c3RlbS9BbGxlcmd5SW50b2xlcmF
uY2UucnMgc3lzdGVtL09yZ2FuaXphdGlvbi5ycyBzeXN0ZW0vUHJhY3RpdGlvbmVy
LnJzIHN5c3RlbS9Db25kaXRpb24ucnMgc3lzdGVtL0NhcmVUZWFtLnJzIHN5c3Rlb
S9JbW11bml6YXRpb24ucnMgc3lzdGVtL1BhdGllbnQucnMgc3lzdGVtL1Byb3Zlbm
FuY2UucnMgc3lzdGVtL0dvYWwucnMgc3lzdGVtL1ByYWN0aXRpb25lclJvbGUucnM
gc3lzdGVtL01lZGljYXRpb25SZXF1ZXN0LnJzIHN5c3RlbS9DYXJlUGxhbi5ycyBv
bmxpbmVfYWNjZXNzIHN5c3RlbS9Eb2N1bWVudFJlZmVyZW5jZS5ycyBzeXN0ZW0vT
G9jYXRpb24ucnMgc3lzdGVtL1Byb2NlZHVyZS5ycyBzeXN0ZW0vT2JzZXJ2YXRpb2
4ucnMgbGF1bmNoL3BhdGllbnQgc3lzdGVtL0RldmljZS5ycyBzeXN0ZW0vTWVkaWN
hdGlvbi5ycyBzeXN0ZW0vRGlhZ25vc3RpY1JlcG9ydC5ycyBvcGVuaWQiLCJhbGxv
d2VkRmhpclVybCI6Imh0dHBzOi8vcG9kMjF0ZXN0Lm1taS5wcm9kLmZoaXIuZW1hL
WFwaS5jb20vZmhpci9yNCIsImNsaWVudEhvc3QiOiIxMC4yMDAuMi4yNTIiLCJjbG
llbnRJZCI6ImZoaXIwMDA2MjM3MTk5MTdhNWMwMDA4ZmEzYjA3MTgyMzE0ZWRlYjB
jZmM4MDQ2MzljZmE1ZSIsImNsaWVudEFkZHJlc3MiOiIxMC4yMDAuMi4yNTIifQ.Q
CIulNFY3fqCw-i7Asp_sBg0FfUkOFNk1GR6UF00C3MrV-fP2ks81S9i1WfUBTpRSi
d3guqyuwWXojvT7YzUFUQbiLdWqzYNPiUJKGqmvKwQFJYjDEPXx0h8armNSCYPK_o
R_GflnrT35zWVn6VJ4AWVvVk3DP9zl38YH5d47bd-b93x-nnREntHxxcDMvAmbRdH
uBGjxTt9c9lO10KGY8MrdX8gdiFl2nHfawq2LiPpT3TVj0DlfAgEBTpz8wiaASkjr
URelX1sjsPeCIsrC21VkOipfyp4IYgp-mRp4MQf6PB1xv_W3RHDwokloDGtt7rkbR
pq9hDlP06jLRYR1g",
"expires_in": 1800,
"refresh_expires_in": 0,
"token_type": "Bearer",
"not-before-policy": 0,
"scope": "launch system/Encounter.rs
system/AllergyIntolerance.rs system/Organization.rs
system/Practitioner.rs system/Condition.rs system/CareTeam.rs
system/Immunization.rs system/Patient.rs system/Provenance.rs
system/Goal.rs system/PractitionerRole.rs
system/MedicationRequest.rs system/CarePlan.rs online_access
system/DocumentReference.rs system/Location.rs
system/Procedure.rs system/Observation.rs launch/patient
system/Device.rs system/Medication.rs system/DiagnosticReport.rs
openid",
"allowedFhirUrl":
"https://pod21test.mmi.prod.fhir.ema-api.com/fhir/r4"
}
```

<br />

**Start the Bulk FHIR Data Request**

Examples:

* \{base\\\_url}/Patient/$export
* \{base\\\_url}/$export?\\\_since=2022-10-01T00:00:00&\\\_outputFormat=ndjson
* \{base\\\_url}/Group/1.105681.22.0.1/$export

The Patient export returns FHIR resources in the USCDI data set.

Vendors will first need to know the base url of the practice they want to integrate with.

When making an export call, parameters of \_since and \_outputFormat are supported.

Only ‘ndjson’ format is supported for the Output.

The parameters supported in the various data sets are shown in the metadata section. The same data available through the USCDI single API calls are supported in the Bulk calls.

If you require a group or cohort of patients, the Patient IDs must be defined and then someone\
at MMI can create a group. Please reach out to [synapsys@modmed.com](mailto:synapsys@modmed.com) for any help with this.

<br />

**Check Status of the Bulk Request**

After making the Bulk API call, the Content-Location will return how to check the status of the Bulk call. Depending on the size of the customer patient database, the calls will take time to return the data, hence checking the status would be necessary.\
Below is an example of how to check the status of a Bulk request that was made

\{base\\\_url}/fhir-services/$export-status/d60cbaa19d337fbfb8ba2677d4dc30a4

After this request is completed, the status API returns the URL for the resource files.\
For example :-
url":"[https://modmed-fhir-batch.s3.us-east-2.amazonaws.com/ema/100491/141be1b64458efc](https://modmed-fhir-batch.s3.us-east-2.amazonaws.com/ema/100491/141be1b64458efc)
c0d7aa3b0154be48a/encounter\_1.ndjson……..

<br />

**Viewing the Resource Files**

Once the Bulk process is done, separate les get generated for each resource. The format of each of the les in ‘ndjson’. Each file contains a maximum of 1000 resources.

Here is a sample of a file for the ‘Medication Request’ Resource.

![](https://files.readme.io/6068ce79a651fecde03e7818150abf72e09294fbdf11bbaaaebd3ba0d0c70531-image.png)

**Deleting the Bulk Request**

If a vendor started a bulk request and then decides to delete the request, we can support that using a delete CALL on the Bulk Request.  &#x20;
\{base\\\_url}/fhir-services/$export-status/d60cbaa19d337fbfb8ba2677d4dc30a4

<br />

**Error Cases**

If vendors try to access les in a dierent format, for example ‘csv’, then we will throw a ‘400 Bad Request’ error as this format is not supported. The error message would state ‘Invalid Tenant’. &#x20;
\{base\\\_url}/$export?\\\_since=2022-10-01T00:00:00&\\\_outputFormat=csv