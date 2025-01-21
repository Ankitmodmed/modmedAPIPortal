---
title: CarePlan
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

<br />

New content:

Care Plans are versatile tools in healthcare, used for tasks ranging from tracking routine immunizations to managing complex treatment plans, such as oncology care involving chemotherapy, diet, and counseling. They also apply to veterinary care, clinical research, and public health initiatives like education or immunization campaigns.

Read more from: [https://hl7.org/fhir/R4/careplan.html](https://hl7.org/fhir/R4/careplan.html)

<br />

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
```json new json
{
  "resourceType" : "CarePlan",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External Ids for this plan
  "instantiatesCanonical" : [{ canonical(PlanDefinition|Questionnaire|Measure|
   ActivityDefinition|OperationDefinition) }], // Instantiates FHIR protocol or definition
  "instantiatesUri" : ["<uri>"], // Instantiates external protocol or definition
  "basedOn" : [{ Reference(CarePlan) }], // Fulfills CarePlan
  "replaces" : [{ Reference(CarePlan) }], // CarePlan replaced by this CarePlan
  "partOf" : [{ Reference(CarePlan) }], // Part of referenced CarePlan
  "status" : "<code>", // R!  draft | active | on-hold | revoked | completed | entered-in-error | unknown
  "intent" : "<code>", // R!  proposal | plan | order | option
  "category" : [{ CodeableConcept }], // Type of plan
  "title" : "<string>", // Human-friendly name for the care plan
  "description" : "<string>", // Summary of nature of plan
  "subject" : { Reference(Patient|Group) }, // R!  Who the care plan is for
  "encounter" : { Reference(Encounter) }, // Encounter created as part of
  "period" : { Period }, // Time period plan covers
  "created" : "<dateTime>", // Date record was first recorded
  "author" : { Reference(Patient|Practitioner|PractitionerRole|Device|
   RelatedPerson|Organization|CareTeam) }, // Who is the designated responsible party
  "contributor" : [{ Reference(Patient|Practitioner|PractitionerRole|Device|
   RelatedPerson|Organization|CareTeam) }], // Who provided the content of the care plan
  "careTeam" : [{ Reference(CareTeam) }], // Who's involved in plan?
  "addresses" : [{ Reference(Condition) }], // Health issues this plan addresses
  "supportingInfo" : [{ Reference(Any) }], // Information considered as part of plan
  "goal" : [{ Reference(Goal) }], // Desired outcome of plan
  "activity" : [{ // Action to occur as part of plan
    "outcomeCodeableConcept" : [{ CodeableConcept }], // Results of the activity
    "outcomeReference" : [{ Reference(Any) }], // Appointment, Encounter, Procedure, etc.
    "progress" : [{ Annotation }], // Comments about the activity status/progress
    "reference" : { Reference(Appointment|CommunicationRequest|DeviceRequest|
    MedicationRequest|NutritionOrder|Task|ServiceRequest|VisionPrescription|
    RequestGroup) }, // C? Activity details defined in specific resource
    "detail" : { // C? In-line definition of activity
      "kind" : "<code>", // Appointment | CommunicationRequest | DeviceRequest | MedicationRequest | NutritionOrder | Task | ServiceRequest | VisionPrescription
      "instantiatesCanonical" : [{ canonical(PlanDefinition|ActivityDefinition|
     Questionnaire|Measure|OperationDefinition) }], // Instantiates FHIR protocol or definition
      "instantiatesUri" : ["<uri>"], // Instantiates external protocol or definition
      "code" : { CodeableConcept }, // Detail type of activity
      "reasonCode" : [{ CodeableConcept }], // Why activity should be done or why activity was prohibited
      "reasonReference" : [{ Reference(Condition|Observation|DiagnosticReport|
     DocumentReference) }], // Why activity is needed
      "goal" : [{ Reference(Goal) }], // Goals this activity relates to
      "status" : "<code>", // R!  not-started | scheduled | in-progress | on-hold | completed | cancelled | stopped | unknown | entered-in-error
      "statusReason" : { CodeableConcept }, // Reason for current status
      "doNotPerform" : <boolean>, // If true, activity is prohibiting action
      // scheduled[x]: When activity is to occur. One of these 3:
      "scheduledTiming" : { Timing },
      "scheduledPeriod" : { Period },
      "scheduledString" : "<string>",
      "location" : { Reference(Location) }, // Where it should happen
      "performer" : [{ Reference(Practitioner|PractitionerRole|Organization|
     RelatedPerson|Patient|CareTeam|HealthcareService|Device) }], // Who will be responsible?
      // product[x]: What is to be administered/supplied. One of these 2:
      "productCodeableConcept" : { CodeableConcept },
      "productReference" : { Reference(Medication|Substance) },
      "dailyAmount" : { Quantity(SimpleQuantity) }, // How to consume/day?
      "quantity" : { Quantity(SimpleQuantity) }, // How much to administer/supply/consume
      "description" : "<string>" // Extra info describing activity to perform
    }
  }],
  "note" : [{ Annotation }] // Comments about the plan
}
```