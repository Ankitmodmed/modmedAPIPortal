---
title: Observation
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
Base profile: <http://hl7.org/fhir/observation.html>

The FHIR Observation endpoint typically returns data about clinical measurements taken on patients, such as vital signs, body measurements, lab results, and so on.

## Key Fields

- **resourceType:** Identifies the type of the resource (e.g., "Observation").
- **id:** Unique identifier for the observation resource.
- **status:** The status of the observation (e.g., "final").
- **category:** Classifies the general type of observation (e.g., vital-signs).
- **code:** The specific observation being reported (e.g., blood pressure).
- **subject:** The subject of the observation (typically a reference to a Patient).
- **effectiveDateTime:** The date and time when the observation was made.
- **valueQuantity:** The result of the observation, including the value and the unit of measurement.

**Sample Response Object:**

```Text json
{
  "resourceType": "Observation",
  "id": "example",
  "status": "final",
  "category": [
    {
      "coding": [
        {
          "system": "http://terminology.hl7.org/CodeSystem/observation-category",
          "code": "vital-signs",
          "display": "Vital Signs"
        }
      ]
    }
  ],
  "code": {
    "coding": [
      {
        "system": "http://loinc.org",
        "code": "85354-9",
        "display": "Blood pressure panel with all children optional"
      }
    ],
    "text": "Blood Pressure"
  },
  "subject": {
    "reference": "Patient/example"
  },
  "effectiveDateTime": "2012-09-17",
  "valueQuantity": {
    "value": 120,
    "unit": "mmHg",
    "system": "http://unitsofmeasure.org",
    "code": "mm[Hg]"
  }
}
```