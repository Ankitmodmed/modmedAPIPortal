---
title: Condition
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-condition](http://hl7.org/fhir/us/core/StructureDefinition/us-core-condition)

The Condition endpoint in FHIR is used to capture and share clinical conditions/problems/diagnoses associated with patients.

The key components for a FHIR Condition endpoint typically include the following fields:

1. **resourceType**: Identifies this resource as a Condition resource.

2. **id**: A unique identifier for the condition instance.

3. **clinicalStatus**: Indicates the clinical status of the condition (e.g., active, recurrence, remission).

4. **verificationStatus**: Indicates whether the condition is confirmed, unconfirmed, differential diagnosis, etc.

5. **category**: Specifies a category for the condition. Common categories might include problem-list-item, encounter-diagnosis, etc.

6. **severity**: Optional field to indicate the severity of the condition.

7. **code**: A code that represents the condition, often from standard coding systems like SNOMED CT, ICD-10, etc.

8. **bodySite**: Indicates the anatomical location associated with this condition.

9. **subject**: Reference to the patient to whom the condition belongs.

10. **encounter**: Reference to the encounter during which the condition was diagnosed.

11. **onset\[x]**: The estimated or actual date, age, or period when the condition began.

12. **abatement\[x]**: The estimated or actual date, age, or period when the condition resolved or went into remission.

13. **recordedDate**: The date when the condition was recorded.

14. **recorder**: Reference to the practitioner or individual who recorded the condition.

15. **asserter**: Reference to the practitioner or individual who asserts this condition, which may be different from the recorder.

16. **stage**: Information about the stage or severity of the condition.

17. **evidence**: Supporting information to demonstrate the existence of the condition.

18. **note**: Additional information about the condition.

<br />

New content:

Condition resource is used to record detailed information about a condition, problem, diagnosis, or other event, situation, issue, or clinical concept that has risen to a level of concern.

<br />

Here's a concise JSON structure showcasing these components:

**Sample Response Object:**

```Text json
{  
  "resourceType": "Condition",  
  "id": "example",  
  "clinicalStatus": {  
    "coding": [  
      {  
        "system": "http://terminology.hl7.org/CodeSystem/condition-clinical",  
        "code": "active"  
      }  
    ]  
  },  
  "verificationStatus": {  
    "coding": [  
      {  
        "system": "http://terminology.hl7.org/CodeSystem/condition-ver-status",  
        "code": "confirmed"  
      }  
    ]  
  },  
  "category": \[  
    {  
      "coding": [  
        {  
          "system": "http://terminology.hl7.org/CodeSystem/condition-category",  
          "code": "problem-list-item",  
          "display": "Problem List Item"  
        }  
      ]  
    }  
  ],  
  "code": {  
    "coding": [  
      {  
        "system": "http://snomed.info/sct",  
        "code": "386661006",  
        "display": "Fever"  
      }  
    ],  
    "text": "Fever"  
  },  
  "subject": {  
    "reference": "Patient/example",  
    "display": "Example Patient"  
  },  
  "onsetDateTime": "2020-03-03T00:00:00+00:00",  
  "recordedDate": "2020-03-03T00:00:00+00:00",  
  "recorder": {  
    "reference": "Practitioner/example",  
    "display": "Dr. John Smith"  
  }  
}
```
```json new json
{
  "resourceType" : "Condition",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External Ids for this condition
  "clinicalStatus" : { CodeableConcept }, // C? active | recurrence | relapse | inactive | remission | resolved
  "verificationStatus" : { CodeableConcept }, // C? unconfirmed | provisional | differential | confirmed | refuted | entered-in-error
  "category" : [{ CodeableConcept }], // problem-list-item | encounter-diagnosis
  "severity" : { CodeableConcept }, // Subjective severity of condition
  "code" : { CodeableConcept }, // Identification of the condition, problem or diagnosis
  "bodySite" : [{ CodeableConcept }], // Anatomical location, if relevant
  "subject" : { Reference(Patient|Group) }, // R!  Who has the condition?
  "encounter" : { Reference(Encounter) }, // Encounter created as part of
  // onset[x]: Estimated or actual date,  date-time, or age. One of these 5:
  "onsetDateTime" : "<dateTime>",
  "onsetAge" : { Age },
  "onsetPeriod" : { Period },
  "onsetRange" : { Range },
  "onsetString" : "<string>",
  // abatement[x]: When in resolution/remission. One of these 5:
  "abatementDateTime" : "<dateTime>",
  "abatementAge" : { Age },
  "abatementPeriod" : { Period },
  "abatementRange" : { Range },
  "abatementString" : "<string>",
  "recordedDate" : "<dateTime>", // Date record was first recorded
  "recorder" : { Reference(Practitioner|PractitionerRole|Patient|
   RelatedPerson) }, // Who recorded the condition
  "asserter" : { Reference(Practitioner|PractitionerRole|Patient|
   RelatedPerson) }, // Person who asserts this condition
  "stage" : [{ // Stage/grade, usually assessed formally
    "summary" : { CodeableConcept }, // C? Simple summary (disease specific)
    "assessment" : [{ Reference(ClinicalImpression|DiagnosticReport|Observation) }], // C? Formal record of assessment
    "type" : { CodeableConcept } // Kind of staging
  }],
  "evidence" : [{ // Supporting evidence
    "code" : [{ CodeableConcept }], // C? Manifestation/symptom
    "detail" : [{ Reference(Any) }] // C? Supporting information found elsewhere
  }],
  "note" : [{ Annotation }] // Additional information about the Condition
}
```