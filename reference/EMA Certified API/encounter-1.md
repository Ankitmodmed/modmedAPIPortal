---
title: Encounter
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
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-encounter>

The FHIR (Fast Healthcare Interoperability Resources) Encounter resource is used to record an interaction between a patient and healthcare provider(s) during which services are provided. A FHIR Encounter endpoint typically deals with the creation, retrieval, and management of these interactions. Below are key components and a sample response of a FHIR Encounter endpoint:

### Key Components of FHIR Encounter

- **id**: A unique identifier for the encounter.
- **status**: The current state of the encounter (e.g., planned, arrived, in-progress, etc.).
- **class**: The classification of the encounter (e.g., outpatient, inpatient).
- **type**: Specific type of encounter (e.g., emergency, consultation).
- **subject**: The patient involved in the encounter.
- **participant**: The individuals involved in the encounter other than the patient (e.g., practitioners).
- **period**: The start and end time of the encounter.
- **location**: The location(s) where the encounter took place.
- **reasonCode**: The reason for the encounter.
- **diagnosis**: Information about the diagnosis during the encounter.

**Sample Response Object:**

```Text json
{
  "resourceType": "Encounter",
  "id": "encounter-example-1",
  "status": "finished",
  "class": {
    "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
    "code": "AMB",
    "display": "ambulatory"
  },
  "type": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "185349003",
          "display": "Encounter for check up"
        }
      ]
    }
  ],
  "subject": {
    "reference": "Patient/patient-example-1"
  },
  "participant": [
    {
      "individual": {
        "reference": "Practitioner/practitioner-example-1"
      }
    }
  ],
  "period": {
    "start": "2021-01-01T09:00:00Z",
    "end": "2021-01-01T09:30:00Z"
  },
  "location": [
    {
      "location": {
        "reference": "Location/location-example-1",
        "display": "Main Hospital"
      }
    }
  ],
  "reasonCode": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "183947004",
          "display": "General examination of patient"
        }
      ]
    }
  ],
  "diagnosis": [
    {
      "condition": {
        "reference": "Condition/condition-example-1"
      }
    }
  ]
}
```

This representation captures the essence of an Encounter resource in FHIR, including relevant patient information, the type and status of the encounter, and the healthcare providers involved.