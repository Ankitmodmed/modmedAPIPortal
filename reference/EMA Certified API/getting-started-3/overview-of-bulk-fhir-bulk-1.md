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