---
title: ServiceRequest
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-servicerequest](http://hl7.org/fhir/us/core/StructureDefinition/us-core-servicerequest)

The FHIR (Fast Healthcare Interoperability Resources) ServiceRequest resource is used to describe a request for a service to be performed. This might include diagnostic tests, procedures, or other healthcare-related services.

## Key Components of a ServiceRequest Resource

* **ID**: Unique identifier for the request.
* **Status**: The status of the request (e.g., active, completed, draft).
* **Intent**: The purpose or intention behind the request (e.g., order, original-order).
* **Code**: The specific service being requested, often represented with a code.
* **Subject**: The patient whom the service is being requested for.
* **Requester**: The individual or organization making the request.
* **ReasonCode**: The rationale or justification for the request.

New content:

ServiceRequest is a record of a request for a procedure or diagnostic or other service to be planned, proposed, or performed.

Read more from: [https://hl7.org/fhir/R4/servicerequest.html](https://hl7.org/fhir/R4/servicerequest.html)

**Sample Response Object:**

```Text json
{
  "resourceType": "ServiceRequest",
  "id": "example",
  "status": "active",
  "intent": "order",
  "code": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "104001",
        "display": "Haemoglobinometry"
      }
    ],
    "text": "Haemoglobinometry"
  },
  "subject": {
    "reference": "Patient/12345",
    "display": "John Doe"
  },
  "requester": {
    "reference": "Practitioner/67890",
    "display": "Dr. Smith"
  },
  "reasonCode": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "28032008",
          "display": "Anemia"
        }
      ],
      "text": "Anemia"
    }
  ]
}
```
```json new json
{
  "resourceType" : "ServiceRequest",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Identifiers assigned to this order
  "instantiatesCanonical" : [{ canonical(ActivityDefinition|PlanDefinition) }], // Instantiates FHIR protocol or definition
  "instantiatesUri" : ["<uri>"], // Instantiates external protocol or definition
  "basedOn" : [{ Reference(CarePlan|ServiceRequest|MedicationRequest) }], // What request fulfills
  "replaces" : [{ Reference(ServiceRequest) }], // What request replaces
  "requisition" : { Identifier }, // Composite Request ID
  "status" : "<code>", // R!  draft | active | on-hold | revoked | completed | entered-in-error | unknown
  "intent" : "<code>", // R!  proposal | plan | directive | order | original-order | reflex-order | filler-order | instance-order | option
  "category" : [{ CodeableConcept }], // Classification of service
  "priority" : "<code>", // routine | urgent | asap | stat
  "doNotPerform" : <boolean>, // True if service/procedure should not be performed
  "code" : { CodeableConcept }, // What is being requested/ordered
  "orderDetail" : [{ CodeableConcept }], // C? Additional order information
  // quantity[x]: Service amount. One of these 3:
  "quantityQuantity" : { Quantity },
  "quantityRatio" : { Ratio },
  "quantityRange" : { Range },
  "subject" : { Reference(Patient|Group|Location|Device) }, // R!  Individual or Entity the service is ordered for
  "encounter" : { Reference(Encounter) }, // Encounter in which the request was created
  // occurrence[x]: When service should occur. One of these 3:
  "occurrenceDateTime" : "<dateTime>",
  "occurrencePeriod" : { Period },
  "occurrenceTiming" : { Timing },
  // asNeeded[x]: Preconditions for service. One of these 2:
  "asNeededBoolean" : <boolean>,
  "asNeededCodeableConcept" : { CodeableConcept },
  "authoredOn" : "<dateTime>", // Date request signed
  "requester" : { Reference(Practitioner|PractitionerRole|Organization|
   Patient|RelatedPerson|Device) }, // Who/what is requesting service
  "performerType" : { CodeableConcept }, // Performer role
  "performer" : [{ Reference(Practitioner|PractitionerRole|Organization|
   CareTeam|HealthcareService|Patient|Device|RelatedPerson) }], // Requested performer
  "locationCode" : [{ CodeableConcept }], // Requested location
  "locationReference" : [{ Reference(Location) }], // Requested location
  "reasonCode" : [{ CodeableConcept }], // Explanation/Justification for procedure or service
  "reasonReference" : [{ Reference(Condition|Observation|DiagnosticReport|
   DocumentReference) }], // Explanation/Justification for service or service
  "insurance" : [{ Reference(Coverage|ClaimResponse) }], // Associated insurance coverage
  "supportingInfo" : [{ Reference(Any) }], // Additional clinical information
  "specimen" : [{ Reference(Specimen) }], // Procedure Samples
  "bodySite" : [{ CodeableConcept }], // Location on Body
  "note" : [{ Annotation }], // Comments
  "patientInstruction" : "<string>", // Patient or consumer-oriented instructions
  "relevantHistory" : [{ Reference(Provenance) }] // Request provenance
}
```