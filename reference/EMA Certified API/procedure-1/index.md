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

The Procedure resource in FHIR represents an action that is being, has been, or is scheduled to be performed on a patient. Examples of procedures include surgeries, therapies, diagnostic actions, and more.

## Key Components of FHIR Procedure Resource

1. **Identifier**: Unique identifier for the procedure.
2. **Status**: Indicates the current state of the procedure (e.g., preparation, in progress, completed, entered-in-error, etc.).
3. **Category**: Broad categorization of the type of procedure (e.g., surgical, laboratory, etc.).
4. **Code**: A specific code or description identifying the procedure.
5. **Subject**: The patient, implying whom the procedure is performed on.
6. **Encounter**: The encounter during which the procedure was performed.
7. **Performed**: The period of time during which the procedure was performed.
8. **Performer**: Individual(s) who performed the procedure.
9. **ReasonCode**: The reason why the procedure was performed.
10. **BodySite**: Target body site where the procedure was performed.
11. **Outcome**: The result or outcome of the procedure.
12. **Report**: Any report generated as a result of the procedure.
13. **Complication**: Any complications experienced during the procedure.
14. **FollowUp**: Instructions or information regarding follow-up care.

<br />

New content:

Procedure resource is used to record the details of current and historical procedures performed on or for a patient. A procedure is an activity that is performed on, with, or for a patient as part of the provision of care.

Read more from: [https://hl7.org/fhir/R4/procedure.html](https://hl7.org/fhir/R4/procedure.html)

**Sample Response Object:**

```Text json
{
 "resourceType": "Procedure",
 "id": "example",
 "status": "completed",
 "category": {
   "coding": [
     {
       "system": "http://snomed.info/sct",
       "code": "103693007",
       "display": "Diagnostic procedure"
     }
   ],
   "text": "Diagnostic procedure"
 },
 "code": {
   "coding": [
     {
       "system": "http://snomed.info/sct",
       "code": "80146002",
       "display": "Appendectomy"
     }
   ],
   "text": "Appendectomy"
 },
 "subject": {
   "reference": "Patient/example"
 },
 "encounter": {
   "reference": "Encounter/example"
 },
 "performedPeriod": {
   "start": "2014-08-16T06:00:00Z",
   "end": "2014-08-16T07:30:00Z"
 },
 "performer": [
   {
     "actor": {
       "reference": "Practitioner/example",
       "display": "Dr. John Doe"
     },
     "role": {
       "coding": [
         {
           "system": "http://terminology.hl7.org/CodeSystem/v2-0412",
           "code": "01",
           "display": "Primary surgeon"
         }
       ]
     }
   }
 ],
 "reasonCode": [
   {
     "coding": [
       {
         "system": "http://snomed.info/sct",
         "code": "233604007",
         "display": "Acute appendicitis"
       }
     ],
     "text": "Acute appendicitis"
   }
 ],
 "outcome": {
   "coding": [
     {
       "system": "http://snomed.info/sct",
       "code": "301608005",
       "display": "Appendix removed"
     }
   ],
"text": "Appendix removed"
 }
}
```
```json new json
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