---
title: Updates Patient Resource
excerpt: ''
api:
  file: ema-proprietary-api.json
  operationId: put_patient-id
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Updates Patient Resource.

In the body of HTTP PUT, you can send in valid FHIR Patient information to update as JSON (be sure to include the "ID" element for the Patient).

**NOTE:** You will only send the values that you want to update. So you do not need to send a full FHIR Patient object like you did for Patient Create.

### Return Preferences for Updating Patient Resource:

* **FHIR Representation:**\
  To receive a FHIR representation of the newly updated patient, include the following header in your request:
  * Header: `Prefer`
  * Value: `return=representation`
* **Operation Outcome:**\
  If you prefer to receive only an Operation Outcome with details of the updated patient, use the following header:
  * Header: `Prefer`
  * Value: `return=OperationOutcome`
* **Default Behavior:**\
  If no return preference header is specified, the default response for a successfully updated patient will be an HTTP `201 Created` status code. The response headers will contain the necessary information to look up the newly created patient:
  * `Content-Location`: `{base_url}/{firm_url_prefix}/ema/fhir/v2/Patient/5199`
  * `Location`: `{base_url}/{firm_url_prefix}/ema/fhir/v2/Patient/5199`
* **Error Handling:**\
  If the patient creation fails due to validation errors, the response will include an Operation Outcome along with an appropriate HTTP status code.