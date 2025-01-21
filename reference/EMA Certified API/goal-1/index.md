---
title: Goal
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-goal](http://hl7.org/fhir/us/core/StructureDefinition/us-core-goal)

The FHIR (Fast Healthcare Interoperability Resources) Goal resource is used to define specific goals for a patient, such as treatment goals, behavioral change goals, or other types of health-related objectives. The Goal endpoint in an FHIR API allows clients to retrieve and manage these goals.

### Key Components of a FHIR Goal Resource

1. **id**: Unique identifier for the goal.
2. **meta**: Metadata about the resource, including version, last updated time, etc.
3. **status**: Indicates the current status of the goal (e.g., proposed, accepted, planned, in-progress, on-target, ahead-of-target, behind-target, suspended, cancelled, completed, entered-in-error, rejected).
4. **description**: A detailed description of the goal, often in natural language.
5. **subject**: Reference to the patient or other entity to whom this goal is associated.
6. **startDate**: The date when the goal was defined.
7. **target**: Sub-component that specifies target outcomes, dates, and other measures.
8. **category**: Categorical descriptor for the goal (e.g., dietary, behavioral, etc.).
9. **priority**: The priority of the goal (e.g., high-priority, medium-priority).
10. **addresses**: References to conditions/problem statements/issues being addressed by the goal.
11. **note**: Comments or notes about the goal.

<br />

New content:

A goal represents a specific goal instance for a particular patient, group, etc. It is not intended to be used to define types of potential goals as part of an order set or protocol definition.

The Goal resource is intended to be used once an order set is instantiated or assigned to a patient, which is when the potential goals become the actual goals, if not changed or deleted.

Read more from : [https://hl7.org/fhir/R4/goal.html](https://hl7.org/fhir/R4/goal.html)

<br />

**Sample Response Object:**

```Text json
{  
  "resourceType": "Goal",  
  "id": "example",  
  "status": "in-progress",  
  "description": {  
    "text": "Achieve a weight loss of 10 kg over the next 6 months"  
  },  
  "subject": {  
    "reference": "Patient/12345",  
    "display": "John Doe"  
  },  
  "startDate": "2023-01-01",  
  "target": \[  
    {  
      "measure": {  
        "coding": [  
          {  
            "system": "http://loinc.org",  
            "code": "29463-7",  
            "display": "Body Weight"  
          }  
        ],  
        "text": "Body Weight"  
      },  
      "detailQuantity": {  
        "value": 70,  
        "unit": "kg",  
        "system": "<http://unitsofmeasure.org">,  
        "code": "kg"  
      },  
      "dueDate": "2023-07-01"  
    }  
  ],  
  "category": \[  
    {  
      "coding": [  
        {  
          "system": "http://hl7.org/fhir/goal-category",  
          "code": "dietary",  
          "display": "Dietary"  
        }  
      ]  
    }  
  ],  
  "priority": {  
    "coding": [  
      {  
        "system": "http://hl7.org/fhir/goal-priority",  
        "code": "high-priority",  
        "display": "High Priority"  
      }  
    ]  
  },  
  "addresses": [  
    {  
      "reference": "Condition/67890",  
      "display": "Obesity"  
    }  
  ],  
  "note": [  
    {  
      "text": "Patient is motivated and has strong family support."  
    }  
  ]  
}
```
```json new json
{
  "resourceType" : "Goal",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External Ids for this goal
  "lifecycleStatus" : "<code>", // R!  proposed | planned | accepted | active | on-hold | completed | cancelled | entered-in-error | rejected
  "achievementStatus" : { CodeableConcept }, // in-progress | improving | worsening | no-change | achieved | sustaining | not-achieved | no-progress | not-attainable
  "category" : [{ CodeableConcept }], // E.g. Treatment, dietary, behavioral, etc.
  "priority" : { CodeableConcept }, // high-priority | medium-priority | low-priority
  "description" : { CodeableConcept }, // R!  Code or text describing goal
  "subject" : { Reference(Patient|Group|Organization) }, // R!  Who this goal is intended for
  // start[x]: When goal pursuit begins. One of these 2:
  "startDate" : "<date>",
  "startCodeableConcept" : { CodeableConcept },
  "target" : [{ // C? Target outcome for the goal
    "measure" : { CodeableConcept }, // C? The parameter whose value is being tracked
    // detail[x]: The target value to be achieved. One of these 7:
    "detailQuantity" : { Quantity },
    "detailRange" : { Range },
    "detailCodeableConcept" : { CodeableConcept },
    "detailString" : "<string>",
    "detailBoolean" : <boolean>,
    "detailInteger" : <integer>,
    "detailRatio" : { Ratio },
    // due[x]: Reach goal on or before. One of these 2:
    "dueDate" : "<date>"
    "dueDuration" : { Duration }
  }],
  "statusDate" : "<date>", // When goal status took effect
  "statusReason" : "<string>", // Reason for current status
  "expressedBy" : { Reference(Patient|Practitioner|PractitionerRole|
   RelatedPerson) }, // Who's responsible for creating Goal?
  "addresses" : [{ Reference(Condition|Observation|MedicationStatement|
   NutritionOrder|ServiceRequest|RiskAssessment) }], // Issues addressed by this goal
  "note" : [{ Annotation }], // Comments about the goal
  "outcomeCode" : [{ CodeableConcept }], // What result was achieved regarding the goal?
  "outcomeReference" : [{ Reference(Observation) }] // Observation that resulted from goal
}
```

This example provides a comprehensive look at a single goal resource, specifying a patient's goal to achieve a particular weight by a specific date, along with other relevant details.