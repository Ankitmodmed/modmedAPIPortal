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

<br />

New content:

MedicationRequest resource covers all type of orders for medications for a patient. This includes inpatient medication orders as well as community orders.

Read more from: [https://hl7.org/fhir/R4/medicationrequest.html](https://hl7.org/fhir/R4/medicationrequest.html)

<br />

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
```json new json
{
  "resourceType" : "MedicationRequest",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External ids for this request
  "status" : "<code>", // R!  active | on-hold | cancelled | completed | entered-in-error | stopped | draft | unknown
  "statusReason" : { CodeableConcept }, // Reason for current status
  "intent" : "<code>", // R!  proposal | plan | order | original-order | reflex-order | filler-order | instance-order | option
  "category" : [{ CodeableConcept }], // Type of medication usage
  "priority" : "<code>", // routine | urgent | asap | stat
  "doNotPerform" : <boolean>, // True if request is prohibiting action
  // reported[x]: Reported rather than primary record. One of these 2:
  "reportedBoolean" : <boolean>,
  "reportedReference" : { Reference(Patient|Practitioner|PractitionerRole|
   RelatedPerson|Organization) },
  // medication[x]: Medication to be taken. One of these 2:
  "medicationCodeableConcept" : { CodeableConcept },
  "medicationReference" : { Reference(Medication) },
  "subject" : { Reference(Patient|Group) }, // R!  Who or group medication request is for
  "encounter" : { Reference(Encounter) }, // Encounter created as part of encounter/admission/stay
  "supportingInformation" : [{ Reference(Any) }], // Information to support ordering of the medication
  "authoredOn" : "<dateTime>", // When request was initially authored
  "requester" : { Reference(Practitioner|PractitionerRole|Organization|
   Patient|RelatedPerson|Device) }, // Who/What requested the Request
  "performer" : { Reference(Practitioner|PractitionerRole|Organization|
   Patient|Device|RelatedPerson|CareTeam) }, // Intended performer of administration
  "performerType" : { CodeableConcept }, // Desired kind of performer of the medication administration
  "recorder" : { Reference(Practitioner|PractitionerRole) }, // Person who entered the request
  "reasonCode" : [{ CodeableConcept }], // Reason or indication for ordering or not ordering the medication
  "reasonReference" : [{ Reference(Condition|Observation) }], // Condition or observation that supports why the prescription is being written
  "instantiatesCanonical" : ["<canonical>"], // Instantiates FHIR protocol or definition
  "instantiatesUri" : ["<uri>"], // Instantiates external protocol or definition
  "basedOn" : [{ Reference(CarePlan|MedicationRequest|ServiceRequest|
   ImmunizationRecommendation) }], // What request fulfills
  "groupIdentifier" : { Identifier }, // Composite request this is part of
  "courseOfTherapyType" : { CodeableConcept }, // Overall pattern of medication administration
  "insurance" : [{ Reference(Coverage|ClaimResponse) }], // Associated insurance coverage
  "note" : [{ Annotation }], // Information about the prescription
  "dosageInstruction" : [{ Dosage }], // How the medication should be taken
  "dispenseRequest" : { // Medication supply authorization
    "initialFill" : { // First fill details
      "quantity" : { Quantity(SimpleQuantity) }, // First fill quantity
      "duration" : { Duration } // First fill duration
    },
    "dispenseInterval" : { Duration }, // Minimum period of time between dispenses
    "validityPeriod" : { Period }, // Time period supply is authorized for
    "numberOfRepeatsAllowed" : "<unsignedInt>", // Number of refills authorized
    "quantity" : { Quantity(SimpleQuantity) }, // Amount of medication to supply per dispense
    "expectedSupplyDuration" : { Duration }, // Number of days supply per dispense
    "performer" : { Reference(Organization) } // Intended dispenser
  },
  "substitution" : { // Any restrictions on medication substitution
    // allowed[x]: Whether substitution is allowed or not. One of these 2:
    "allowedBoolean" : <boolean>,
    "allowedCodeableConcept" : { CodeableConcept },
    "reason" : { CodeableConcept } // Why should (not) substitution be made
  },
  "priorPrescription" : { Reference(MedicationRequest) }, // An order/prescription that is being replaced
  "detectedIssue" : [{ Reference(DetectedIssue) }], // Clinical Issue with action
  "eventHistory" : [{ Reference(Provenance) }] // A list of events of interest in the lifecycle
}
```