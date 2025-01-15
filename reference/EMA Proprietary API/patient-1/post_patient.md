---
title: Creates Patient Resource
excerpt: ''
api:
  file: ema-proprietary-api.json
  operationId: post_patient
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Creates Patient Resource:

The minimum attributes for creating a patient are:

| Name         | Type   | Description                                                                                                                                                                                                   |
| :----------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| birthdate    | date   | This is the patient's Date of birth - Valid format yyyy-MM-dd                                                                                                                                                 |
| email        | string | A value in an email contact                                                                                                                                                                                   |
| family       | string | This is the patient's last name - Supports exact matches                                                                                                                                                      |
| given        | string | A portion of the given name of the patient                                                                                                                                                                    |
| phone        | string | 10 digit phone number - with or without hyphens                                                                                                                                                               |
| Universal Id | string | Optional. This value should uniquely identify the patient within the managing organization and should not be re-used for other patients. The same value should always be used when updating the same patient. |

### Return Preferences for Created Patient Resource:

* **FHIR Representation:**\
  To receive a FHIR representation of the newly created patient, include the following header in your request:
  * Header: `Prefer`
  * Value: `return=representation`
* **Operation Outcome:**\
  If you prefer to receive only an Operation Outcome with details of the created patient, use the following header:
  * Header: `Prefer`
  * Value: `return=OperationOutcome`
* **Default Behavior:**\
  If no return preference header is specified, the default response for a successfully created patient will be an HTTP `201 Created` status code. The response headers will contain the necessary information to look up the newly created patient:
  * `Content-Location`: `{base_url}/{firm_url_prefix}/ema/fhir/v2/Patient/5199`
  * `Location`: `{base_url}/{firm_url_prefix}/ema/fhir/v2/Patient/5199`
* **Error Handling:**\
  If the patient creation fails due to validation errors, the response will include an Operation Outcome along with an appropriate HTTP status code.
