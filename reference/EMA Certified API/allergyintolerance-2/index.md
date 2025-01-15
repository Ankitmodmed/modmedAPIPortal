---
title: AllergyIntolerance
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-allergyintolerance](http://hl7.org/fhir/us/core/StructureDefinition/us-core-allergyintolerance)

The AllergyIntolerance resource is used to record information about condition-related risk factors. This resource is vital for managing patient allergies and intolerances.

### Key components of the AllergyIntolerance resource include

* **Clinical Status**: Represents the patient's current state regarding the Allergy/Intolerance.
* **Verification Status**: Indicates whether the Allergy/Intolerance has been confirmed.
* **Type**: Differentiates between allergy and intolerance.
* **Category**: Classifies the Allergy/Intolerance into categories such as food, medication, etc.
* **Criticality**: Denotes the potential for life-threatening conditions.
* **Code**: The specific substance or agent causing the reaction.
* **Reaction**: Details about specific adverse reactions including severity, manifestations, and other relevant facts.
* **Patient**: The individual to whom the Allergy/Intolerance is recorded.

**Sample Response Object:**

```Text json
{
  "resourceType": "AllergyIntolerance",
  "id": "example",
  "clinicalStatus": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/allergyintolerance-clinical",
        "code": "active"
      }
    ]
  },
  "verificationStatus": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/allergyintolerance-verification",
        "code": "confirmed"
      }
    ]
  },
  "type": "allergy",
  "category": ["medication"],
  "criticality": "high",
  "code": {
    "coding": [
      {
        "system": "http://www.nlm.nih.gov/research/umls/rxnorm",
        "code": "7980",
        "display": "Penicillin"
      }
    ],
    "text": "Penicillin"
  },
  "patient": {
    "reference": "Patient/example"
  },
  "reaction": [
    {
      "substance": {
        "coding": [
          {
            "system": "http://www.nlm.nih.gov/research/umls/rxnorm",
            "code": "7980",
            "display": "Penicillin"
          }
        ],
        "text": "Penicillin"
      },
      "manifestation": [
        {
          "coding": [
            {
              "system": "http://snomed.info/sct",
              "code": "247472004",
              "display": "Hives"
            }
          ],
          "text": "Hives"
        }
      ],
      "description": "Patient noted hives after taking penicillin.",
      "severity": "moderate"
    }
  ]
}
```
