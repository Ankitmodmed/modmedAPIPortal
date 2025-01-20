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