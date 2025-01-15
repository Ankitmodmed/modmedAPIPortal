---
title: MedicationRequest
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-medicationrequest](http://hl7.org/fhir/us/core/StructureDefinition/us-core-medicationrequest)

The FHIR (Fast Healthcare Interoperability Resources) MedicationRequest resource is used to request medication for a patient. It covers the prescription of medication to a patient, whether it is intended to be taken by them or administered to them.

### Key Components of MedicationRequest

* **id**: A unique identifier for the medication request.
* **status**: The status of the medication request (e.g., active, completed, or stopped).
* **intent**: Indicates the intention behind the medication request (e.g., order or plan).
* **medicationCodeableConcept**: The medication to be taken, identified by a code or name.
* **subject**: The patient for whom the medication request is intended.
* **authoredOn**: The date and time when the request was created.
* **requester**: The healthcare provider or organization who requested the medication.
* **dosageInstruction**: Instructions on how the medication should be taken.
* **dispenseRequest**: Details on how the medication is to be supplied, including quantity and expected supply duration.

**Sample Response Object:**

```Text json
{
  "resourceType": "MedicationRequest",
  "id": "example-medicationrequest",
  "status": "active",
  "intent": "order",
  "medicationCodeableConcept": {
    "coding": [
      {
        "system": "http://www.nlm.nih.gov/research/umls/rxnorm",
        "code": "860975",
        "display": "Amoxicillin 250mg/5ml"
      }
    ],
    "text": "Amoxicillin 250mg/5ml"
  },
  "subject": {
    "reference": "Patient/example",
    "display": "John Doe"
  },
  "authoredOn": "2023-10-01T10:00:00Z",
  "requester": {
    "reference": "Practitioner/example",
    "display": "Dr. Smith"
  },
  "dosageInstruction": [
    {
      "text": "Take 5ml by mouth three times daily",
      "timing": {
        "repeat": {
          "frequency": 3,
          "period": 1,
          "periodUnit": "d"
        }
      },
      "route": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/v3-RouteOfAdministration",
            "code": "PO",
            "display": "By mouth"
          }
        ]
      },
      "doseAndRate": [
        {
          "doseQuantity": {
            "value": 5,
            "unit": "ml",
            "system": "http://unitsofmeasure.org",
            "code": "ml"
          }
        }
      ]
    }
  ],
  "dispenseRequest": {
    "numberOfRepeatsAllowed": 0,
    "quantity": {
      "value": 150,
      "unit": "ml",
      "system": "http://unitsofmeasure.org",
      "code": "ml"
    },
    "expectedSupplyDuration": {
      "value": 10,
      "unit": "days",
      "system": "http://unitsofmeasure.org",
      "code": "d"
    }
  }
}
```
