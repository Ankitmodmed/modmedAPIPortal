---
title: Immunization
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-immunization](http://hl7.org/fhir/us/core/StructureDefinition/us-core-immunization)

The Immunization resource is used to define information related to immunization events in a patient's health record.

### Key Components

1. **Resource Type**: Always "Immunization"
2. **Identifier**: Unique identifiers for the immunization record
3. **Status**: The status of the immunization event (e.g., completed, entered-in-error)
4. **VaccineCode**: The code identifying the vaccine administered
5. **Patient**: Reference to the patient who was immunized
6. **OccurrenceDateTime**: The date and time when the vaccine was administered
7. **Performer**: The individual or organization that provided the immunization
8. **LotNumber**: The lot number of the vaccine dose
9. **Site**: The body site where the vaccine was administered (e.g., left arm)
10. **Route**: The route by which the vaccine was administered (e.g., intramuscular)
11. **DoseQuantity**: The quantity of vaccine administered
12. **Note**: Any additional notes about the immunization event

<br />

New content:

The Immunization resource is intended to cover the recording of current and historical administration of vaccines to patients across all healthcare disciplines in all care settings and all regions. This includes immunization of both humans and animals but does not include the administration of non-vaccine agents, even those that may have or claim to have immunological effects.

Read more from : [https://hl7.org/fhir/R4/immunization.html](https://hl7.org/fhir/R4/immunization.html)

<br />

**Sample Response Object:**

```Text json
{
  "resourceType": "Immunization",
  "id": "example",
  "status": "completed",
  "vaccineCode": {
    "coding": [
      {
        "system": "http://hl7.org/fhir/sid/cvx",
        "code": "03",
        "display": "MMR"
      }
    ]
  },
  "patient": {
    "reference": "Patient/example"
  },
  "occurrenceDateTime": "2022-10-15",
  "primarySource": true,
  "lotNumber": "12345",
  "site": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/v3-ActSite",
        "code": "LA",
        "display": "left arm"
      }
    ]
  },
  "route": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/v3-RouteOfAdministration",
        "code": "IM",
        "display": "Intramuscular"
      }
    ]
  },
  "doseQuantity": {
    "value": 0.5,
    "unit": "mL",
    "system": "http://unitsofmeasure.org",
    "code": "mL"
  },
  "performer": [
    {
      "actor": {
        "reference": "Practitioner/example",
        "display": "Dr. Smith"
      },
      "function": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/v2-0443",
            "code": "OP",
            "display": "Ordering Provider"
          }
        ]
      }
    }
  ],
  "note": [
    {
      "text": "Patient had mild fever after administration"
    }
  ]
}
```
```json new json
{
  "resourceType" : "Immunization",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business identifier
  "status" : "<code>", // R!  completed | entered-in-error | not-done
  "statusReason" : { CodeableConcept }, // Reason not done
  "vaccineCode" : { CodeableConcept }, // R!  Vaccine product administered
  "patient" : { Reference(Patient) }, // R!  Who was immunized
  "encounter" : { Reference(Encounter) }, // Encounter immunization was part of
  // occurrence[x]: Vaccine administration date. One of these 2:
  "occurrenceDateTime" : "<dateTime>",
  "occurrenceString" : "<string>",
  "recorded" : "<dateTime>", // When the immunization was first captured in the subject's record
  "primarySource" : <boolean>, // Indicates context the data was recorded in
  "reportOrigin" : { CodeableConcept }, // Indicates the source of a secondarily reported record
  "location" : { Reference(Location) }, // Where immunization occurred
  "manufacturer" : { Reference(Organization) }, // Vaccine manufacturer
  "lotNumber" : "<string>", // Vaccine lot number
  "expirationDate" : "<date>", // Vaccine expiration date
  "site" : { CodeableConcept }, // Body site vaccine  was administered
  "route" : { CodeableConcept }, // How vaccine entered body
  "doseQuantity" : { Quantity(SimpleQuantity) }, // Amount of vaccine administered
  "performer" : [{ // Who performed event
    "function" : { CodeableConcept }, // What type of performance was done
    "actor" : { Reference(Practitioner|PractitionerRole|Organization) } // R!  Individual or organization who was performing
  }],
  "note" : [{ Annotation }], // Additional immunization notes
  "reasonCode" : [{ CodeableConcept }], // Why immunization occurred
  "reasonReference" : [{ Reference(Condition|Observation|DiagnosticReport) }], // Why immunization occurred
  "isSubpotent" : <boolean>, // Dose potency
  "subpotentReason" : [{ CodeableConcept }], // Reason for being subpotent
  "education" : [{ // Educational material presented to patient
    "documentType" : "<string>", // Educational material document identifier
    "reference" : "<uri>", // Educational material reference pointer
    "publicationDate" : "<dateTime>", // Educational material publication date
    "presentationDate" : "<dateTime>" // Educational material presentation date
  }],
  "programEligibility" : [{ CodeableConcept }], // Patient eligibility for a vaccination program
  "fundingSource" : { CodeableConcept }, // Funding source for the vaccine
  "reaction" : [{ // Details of a reaction that follows immunization
    "date" : "<dateTime>", // When reaction started
    "detail" : { Reference(Observation) }, // Additional information on reaction
    "reported" : <boolean> // Indicates self-reported reaction
  }],
  "protocolApplied" : [{ // Protocol followed by the provider
    "series" : "<string>", // Name of vaccine series
    "authority" : { Reference(Organization) }, // Who is responsible for publishing the recommendations
    "targetDisease" : [{ CodeableConcept }], // Vaccine preventatable disease being targetted
    // doseNumber[x]: Dose number within series. One of these 2:
    "doseNumberPositiveInt" : "<positiveInt>",
    "doseNumberString" : "<string>",
    // seriesDoses[x]: Recommended number of doses for immunity. One of these 2:
    "seriesDosesPositiveInt" : "<positiveInt>"
    "seriesDosesString" : "<string>"
  }]
}
```

This response provides a standardized way to represent information about a given immunization event within a patient's health record.