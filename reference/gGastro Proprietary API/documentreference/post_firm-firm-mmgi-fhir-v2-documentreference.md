---
title: POST  /DocumentReference
excerpt: "Example use:\r\n\r\n POST /DocumentReference\r\n {\r\n   \"fullUrl\": \"{base url}/{firm_url_prefix}/ema/fhir/v2/DocumentReference?patient=7132\",\r\n   \"resourceType\": \"DocumentReference\",\r\n   \"identifier\": \r\n    [{\r\n         \"system\": \"filename\",\r\n         \"value\": \"mikes-file.pdf\"\r\n    }],\r\n   \"status\": \"current\",\r\n   \"type\": {\r\n            \"text\": \"application/pdf\"\r\n    },\r\n   \"category\": \r\n    [{\r\n         \"coding\": \r\n         [{\r\n             \"system\": \"{base url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/document-category\",\r\n             \"code\": \"426\",\r\n             \"display\": \"External Visit Note\"}],\r\n     }],\r\n   \"subject\": {\r\n        \"reference\": \"{base url}/{firm_url_prefix}/Patient/7132\",\r\n        \"display\": \"{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/7132\"\r\n    },\r\n   \"content\": \r\n         [{\r\n               \"attachment\": \r\n               {\r\n                   \"title\": \"Mike's PDF\",\r\n                   \"contentType\": \"application/pdf\",\r\n                   \"url\": \"{generated_s3_url}\",\r\n                   \"size\": 383176,\r\n                   \"creation\": \"2019-04-03T21:11:38+00:00\"\r\n     }\r\n     }]\r\n \r\n }"
api:
  file: mmgi-synapsys-v2.json
  operationId: post_firm-firm-mmgi-fhir-v2-documentreference
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---