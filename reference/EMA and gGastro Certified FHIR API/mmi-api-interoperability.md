---
title: MMI API Interoperability
deprecated: false
hidden: false
metadata:
  robots: index
---
MMI provides access to several APIs for various purposes. This documentation is specific to the Certified FHIR API. For information on MMI's Proprietary API, please see\
[https://www.modmed.com/synapsys-api](https://www.modmed.com/synapsys-api).

By using or accessing any API services or materials, you agree to be bound by the API Terms of Use available at: [https://www.modmed.com/api-terms-of-use/](https://www.modmed.com/api-terms-of-use/)

The main difference between the two APIs relates to use cases and access. The Certified FHIR API Supports two types of API-enabled services:

* Services for which a single patient’s data is the focus
  * A Patient, using their Patient Portal credentials, can authenticate to the API in order to retrieve, access, exchange, or visualize their data.
  * A Provider, using their login credentials, can authenticate to the API in order to retrieve, access, exchange, or visualize a single patient's data.
* Services for which multiple patients’ data are the focus
  * A Provider, using their login credentials, can authenticate to the API in order to retrieve, access, exchange, or visualize multiple patient's data (or a subset of their patient population's data) for population health purposes or insights.
  * Bulk Data Export - a Provider, using their login credentials, can authenticate to the API in order to export (in a standard format - ndjson) multiple patient's data (or a subset of their patient population's data). As of now, this Certified FHIR API supports only Read, Search, and Bulk operations.