---
title: ServiceRequest
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-servicerequest>

The FHIR (Fast Healthcare Interoperability Resources) ServiceRequest resource is used to describe a request for a service to be performed. This might include diagnostic tests, procedures, or other healthcare-related services.

## Key Components of a ServiceRequest Resource

- **ID**: Unique identifier for the request.
- **Status**: The status of the request (e.g., active, completed, draft).
- **Intent**: The purpose or intention behind the request (e.g., order, original-order).
- **Code**: The specific service being requested, often represented with a code.
- **Subject**: The patient whom the service is being requested for.
- **Requester**: The individual or organization making the request.
- **ReasonCode**: The rationale or justification for the request.

**Sample Response Object:**

```Text json
{
  "resourceType": "ServiceRequest",
  "id": "example",
  "status": "active",
  "intent": "order",
  "code": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "104001",
        "display": "Haemoglobinometry"
      }
    ],
    "text": "Haemoglobinometry"
  },
  "subject": {
    "reference": "Patient/12345",
    "display": "John Doe"
  },
  "requester": {
    "reference": "Practitioner/67890",
    "display": "Dr. Smith"
  },
  "reasonCode": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "28032008",
          "display": "Anemia"
        }
      ],
      "text": "Anemia"
    }
  ]
}
```