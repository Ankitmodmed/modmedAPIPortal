---
title: 'search-type: Search for Patient instances'
excerpt: This is a search type
api:
  file: ema-proprietary-api.json
  operationId: get_patient
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

1. Find a patient with a specific first name and last name:  
   GET {base url}/{firm_url_prefix}/ema/fhir/v2/Patient?given=Clayton&family=Abernathy
2. Find a Patient with a specific MRN:  
   GET {base_url}/{firm_url_prefix}/ema/fhir/v2/Patient?identifier=http%3A%2F%2Fwww..hl7.org%2Ffhir%2Fv2%2F0203%2Findex.html%23v2-0203-MR|113940
3. Find a Patient with a specific Race:  
   GET {baseurl}/{firm_url_prefix}/ema/fhir/v2/Patient?us-core-race=http\:://hl7.org/fhir/us/core/STU3/ValueSet-omb-race-category.html|2056-0
4. Find Patients who have a specific Referring Provider  
   GET {base url}/{firm_url_prefix}/ema/fhir/v2/Patient?general-practitioner=Practitioner%2Fref%7C55588
5. Find Patients who have a specific Referral Source  
   GET {base url}/{firm_url_prefix}/ema/fhir/v2/Patient?referral-source=385