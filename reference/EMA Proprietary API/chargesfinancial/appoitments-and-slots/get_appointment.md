---
title: Retrieve All Appointments for a Practice/Firm
excerpt: ''
api:
  file: ema-proprietary-api.json
  operationId: get_appointment
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Examples:

1. GET \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Appointment?\_lastUpdated=ge2020-12-01
2. Example query of Searching for Appointments that have a specific Referring Provider :\
   supporting-info=https%3A%2F%2F\{base\_url}%2Fema%2Ffhir%2Fv2%2FValueSet%2Freferral-source%7C330\&supporting-info=Practitioner/ref%7C68872
3. Example query of Searching for Appointments that have a specific Referring Organization :\
   \{base\_url}/\{firm\_url\_prefix}/ema/fhir/v2/Appointment?supporting-info=Organization/prov%7C451\&patient=27517\&location=299
