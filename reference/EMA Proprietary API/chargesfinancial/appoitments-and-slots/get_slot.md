---
title: Search for a slot
excerpt: ''
api:
  file: ema-proprietary-api.json
  operationId: get_slot
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

1. Search by appointment-type id(mandatory field) :\
   \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Slot?appointment-type=9
2. Search by Identifier: Provider Id :\
   \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Slot?appointment-type=9\&identifier=http\://www\..hl7.org/fhir/v2/0203/index.html#v2-0203-PRN|23
3. Search by Identifier: Facility Id:\
   \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Slot?appointment-type=9\&identifier=http\://www\..hl7.org/fhir/v2/0203/index.html%23v2-0203-FI|23
4. Search by date:\
   \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Slot?appointment-type=9\&date=eq2019-02-21T00:00:00.000Z
5. Search by date range:\
   \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Slot?appointment-type=9\&date=gt2019-02-14T00:00:00.000Z\&date=lt2019-02-16T10:00:00.000Z