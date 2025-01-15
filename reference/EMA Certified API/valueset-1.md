---
title: ValueSet
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
Base Profile: [https://www.hl7.org/fhir/valueset.html](https://www.hl7.org/fhir/valueset.html)

The FHIR Procedure resource is used to record detailed information about actions performed on patients.

## Key Components of the FHIR Procedure Resource

1. **Resource ID**: Unique identifier for the procedure.
2. **Status**: The current state of the procedure (e.g., completed, in-progress).
3. **Code**: The specific code representing the procedure (often using a standardized coding system).
4. **Subject**: The patient subject to the procedure.
5. **Performer**: Who performed the procedure.
6. **Performed**: Date/Period when the procedure was performed.
7. **Reason**: Reason for performing the procedure.
8. **Body Site**: The body site on which the procedure was performed.
9. **Outcome**: The result or outcome of the procedure.

**Sample Response Object:**

```Text json
{
  "resourceType": "Procedure",
  "id": "example",
  "status": "completed",
  "code": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "80146002",
        "display": "Appendectomy (procedure)"
      }
    ],
    "text": "Appendectomy"
  },
  "subject": {
    "reference": "Patient/example"
  },
  "performedPeriod": {
    "start": "2022-02-01T10:30:00+01:00",
    "end": "2022-02-01T11:30:00+01:00"
  },
  "performer": [
    {
      "actor": {
        "reference": "Practitioner/example"
      }
    }
  ],
  "reasonCode": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "233604007",
          "display": "Appendicitis"
        }
      ],
      "text": "Appendicitis"
    }
  ],
  "bodySite": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "78961009",
          "display": "Abdomen"
        }
      ],
      "text": "Abdomen"
    }
  ],
  "outcome": {
    "text": "Procedure was successful"
  }
}
```
