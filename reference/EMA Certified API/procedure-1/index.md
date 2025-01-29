---
title: Procedure
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-procedure](http://hl7.org/fhir/us/core/StructureDefinition/us-core-procedure)

Procedure resource is used to record the details of current and historical procedures performed on or for a patient. A procedure is an activity that is performed on, with, or for a patient as part of the provision of care.

Read more on: [https://hl7.org/fhir/R4/procedure.html](https://hl7.org/fhir/R4/procedure.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "Procedure",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External Identifiers for this procedure
  "instantiatesCanonical" : [{ canonical(PlanDefinition|ActivityDefinition|
   Measure|OperationDefinition|Questionnaire) }], // Instantiates FHIR protocol or definition
  "instantiatesUri" : ["<uri>"], // Instantiates external protocol or definition
  "basedOn" : [{ Reference(CarePlan|ServiceRequest) }], // A request for this procedure
  "partOf" : [{ Reference(Procedure|Observation|MedicationAdministration) }], // Part of referenced event
  "status" : "<code>", // R!  preparation | in-progress | not-done | on-hold | stopped | completed | entered-in-error | unknown
  "statusReason" : { CodeableConcept }, // Reason for current status
  "category" : { CodeableConcept }, // Classification of the procedure
  "code" : { CodeableConcept }, // Identification of the procedure
  "subject" : { Reference(Patient|Group) }, // R!  Who the procedure was performed on
  "encounter" : { Reference(Encounter) }, // Encounter created as part of
  // performed[x]: When the procedure was performed. One of these 5:
  "performedDateTime" : "<dateTime>",
  "performedPeriod" : { Period },
  "performedString" : "<string>",
  "performedAge" : { Age },
  "performedRange" : { Range },
  "recorder" : { Reference(Patient|RelatedPerson|Practitioner|
   PractitionerRole) }, // Who recorded the procedure
  "asserter" : { Reference(Patient|RelatedPerson|Practitioner|
   PractitionerRole) }, // Person who asserts this procedure
  "performer" : [{ // The people who performed the procedure
    "function" : { CodeableConcept }, // Type of performance
    "actor" : { Reference(Practitioner|PractitionerRole|Organization|Patient|
    RelatedPerson|Device) }, // R!  The reference to the practitioner
    "onBehalfOf" : { Reference(Organization) } // Organization the device or practitioner was acting for
  }],
  "location" : { Reference(Location) }, // Where the procedure happened
  "reasonCode" : [{ CodeableConcept }], // Coded reason procedure performed
  "reasonReference" : [{ Reference(Condition|Observation|Procedure|
   DiagnosticReport|DocumentReference) }], // The justification that the procedure was performed
  "bodySite" : [{ CodeableConcept }], // Target body sites
  "outcome" : { CodeableConcept }, // The result of procedure
  "report" : [{ Reference(DiagnosticReport|DocumentReference|Composition) }], // Any report resulting from the procedure
  "complication" : [{ CodeableConcept }], // Complication following the procedure
  "complicationDetail" : [{ Reference(Condition) }], // A condition that is a result of the procedure
  "followUp" : [{ CodeableConcept }], // Instructions for follow up
  "note" : [{ Annotation }], // Additional information about the procedure
  "focalDevice" : [{ // Manipulated, implanted, or removed device
    "action" : { CodeableConcept }, // Kind of change to device
    "manipulated" : { Reference(Device) } // R!  Device that was changed
  }],
  "usedReference" : [{ Reference(Device|Medication|Substance) }], // Items used during procedure
  "usedCode" : [{ CodeableConcept }] // Coded items used during the procedure
}
```