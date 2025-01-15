---
title: Immunization
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-immunization](http://hl7.org/fhir/us/core/StructureDefinition/us-core-immunization)

The Immunization resource is used to define information related to immunization events in a patient's health record.

### Key Components

1. **Resource Type**: Always "Immunization"
2. **Identifier**: Unique identifiers for the immunization record
3. **Status**: The status of the immunization event (e.g., completed, entered-in-error)
4. **VaccineCode**: The code identifying the vaccine administered
5. **Patient**: Reference to the patient who was immunized
6. **OccurrenceDateTime**: The date and time when the vaccine was administered
7. **Performer**: The individual or organization that provided the immunization
8. **LotNumber**: The lot number of the vaccine dose
9. **Site**: The body site where the vaccine was administered (e.g., left arm)
10. **Route**: The route by which the vaccine was administered (e.g., intramuscular)
11. **DoseQuantity**: The quantity of vaccine administered
12. **Note**: Any additional notes about the immunization event

**Sample Response Object:**

```Text json
{
  "resourceType": "Immunization",
  "id": "example",
  "status": "completed",
  "vaccineCode": {
    "coding": [
      {
        "system": "http://hl7.org/fhir/sid/cvx",
        "code": "03",
        "display": "MMR"
      }
    ]
  },
  "patient": {
    "reference": "Patient/example"
  },
  "occurrenceDateTime": "2022-10-15",
  "primarySource": true,
  "lotNumber": "12345",
  "site": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/v3-ActSite",
        "code": "LA",
        "display": "left arm"
      }
    ]
  },
  "route": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/v3-RouteOfAdministration",
        "code": "IM",
        "display": "Intramuscular"
      }
    ]
  },
  "doseQuantity": {
    "value": 0.5,
    "unit": "mL",
    "system": "http://unitsofmeasure.org",
    "code": "mL"
  },
  "performer": [
    {
      "actor": {
        "reference": "Practitioner/example",
        "display": "Dr. Smith"
      },
      "function": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/v2-0443",
            "code": "OP",
            "display": "Ordering Provider"
          }
        ]
      }
    }
  ],
  "note": [
    {
      "text": "Patient had mild fever after administration"
    }
  ]
}
```

This response provides a standardized way to represent information about a given immunization event within a patient's health record.
