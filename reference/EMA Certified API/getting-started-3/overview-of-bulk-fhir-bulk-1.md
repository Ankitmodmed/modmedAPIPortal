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