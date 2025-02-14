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

A goal represents a specific goal instance for a particular patient, group, etc. It is not intended to be used to define types of potential goals as part of an order set or protocol definition.

The Goal resource is intended to be used once an order set is instantiated or assigned to a patient, which is when the potential goals become the actual goals, if not changed or deleted.

Read more from : [https://hl7.org/fhir/R4/goal.html](https://hl7.org/fhir/R4/goal.html)

**Sample Response Object:**

```json json
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