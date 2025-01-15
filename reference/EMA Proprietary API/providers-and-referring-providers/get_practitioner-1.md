---
title: 'search-type: Search for Practitioner instances'
excerpt: This is a search type
api:
  file: ema-proprietary-api.json
  operationId: get_practitioner
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

1. Search for Practitioners by All Possible Search Parameters  
   {baseurl}/{firm_url_prefix}/ema/fhir/v2/Practitioner?email&phone&family=doe&active=true&identifier=http\://www..hl7.org/fhir/v2/0203/index.html%23v2-0203-NPI|1881900637&given=Jane, Mdl
2. Search Practitioners by a Single Parameter  
   {base url}/{firm_url_prefix}/ema/fhir/v2/Practitioner?active=true