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

### General Process

The general process for apps built upon the Certified FHIR API is as follows:

1. Register with MMI: [https://fhir-vendor-dashboard.kube.prod.mmicse.com/](https://fhir-vendor-dashboard.kube.prod.mmicse.com/)
2. Create a Bulk FHIR application:

   ![](https://files.readme.io/9c14d4bca5d46fae761fd8e5d8806622be11d6c57ef69e1e848189457bd32f39-image.png)
3. Your app will be created in a ‘Disabled’ state:

   ![](https://files.readme.io/59539cff7f359afe4a62ca0eec2b8fb69cf515881073cb37a947c18f091ad411-image.png)
4. For Bulk applications, This type of app will require consent from the practice. A Practice can provide your app consent by adding your app’s ClientID to their ‘Manage Bulk FHIR’ section in their Admin section:

   ![](https://files.readme.io/1a59c5a7d046997899857c53c69add16c16b5416ec4b07e26d3c7f692af92acf-image.png)
5. Once a customer has added you, your app will become ‘Enabled’:

   ![](https://files.readme.io/f601c22c78bec58723369a1952ef9d5130735184892431db25426c51d400c93b-image.png)

<br />

**Authentication**

The vendor needs to authenticate with something similar to the following.\
For assistance, [this](https://hl7.org/fhir/smart-app-launch/example-backend-services.html#step-3-access-token) has a good tutorial about how to connect.

POST: \[[https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token\](](https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token]\()[https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token](https://sso.ema.md/auth/realms/fhir/protocol/openid-connect/token)