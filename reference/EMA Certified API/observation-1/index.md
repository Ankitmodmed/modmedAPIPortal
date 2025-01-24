---
title: Observation
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
Base profile: [http://hl7.org/fhir/observation.html](http://hl7.org/fhir/observation.html)

Observation resource contains the Measurements and simple assertions made about a patient, device or other subject.

Read more from: [https://hl7.org/fhir/observation.html](https://hl7.org/fhir/observation.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "Observation",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business Identifier for observation
  // instantiates[x]: Instantiates FHIR ObservationDefinition. One of these 2:
  "instantiatesCanonical" : "<canonical(ObservationDefinition)>",
  "instantiatesReference" : { Reference(ObservationDefinition) },
  "basedOn" : [{ Reference(CarePlan|DeviceRequest|ImmunizationRecommendation|
   MedicationRequest|NutritionOrder|ServiceRequest) }], // Fulfills plan, proposal or order
  "triggeredBy" : [{ // Triggering observation(s)
    "observation" : { Reference(Observation) }, // R!  Triggering observation
    "type" : "<code>", // R!  reflex | repeat | re-run
    "reason" : "<string>" // Reason that the observation was triggered
  }],
  "partOf" : [{ Reference(GenomicStudy|ImagingStudy|Immunization|
   MedicationAdministration|MedicationDispense|MedicationStatement|Procedure) }], // Part of referenced event
  "status" : "<code>", // R!  registered | preliminary | final | amended +
  "category" : [{ CodeableConcept }], // Classification of  type of observation
  "code" : { CodeableConcept }, // I R!  Type of observation (code / type)
  "subject" : { Reference(BiologicallyDerivedProduct|Device|Group|Location|
   Medication|NutritionProduct|Organization|Patient|Practitioner|Procedure|
   Substance) }, // Who and/or what the observation is about
  "focus" : [{ Reference(Any) }], // What the observation is about, when it is not about the subject of record
  "encounter" : { Reference(Encounter) }, // Healthcare event during which this observation is made
  // effective[x]: Clinically relevant time/time-period for observation. One of these 4:
  "effectiveDateTime" : "<dateTime>",
  "effectivePeriod" : { Period },
  "effectiveTiming" : { Timing },
  "effectiveInstant" : "<instant>",
  "issued" : "<instant>", // Date/Time this version was made available
  "performer" : [{ Reference(CareTeam|Organization|Patient|Practitioner|
   PractitionerRole|RelatedPerson) }], // Who is responsible for the observation
  // value[x]: Actual result. One of these 13:
  "valueQuantity" : { Quantity },
  "valueCodeableConcept" : { CodeableConcept },
  "valueString" : "<string>",
  "valueBoolean" : <boolean>,
  "valueInteger" : <integer>,
  "valueRange" : { Range },
  "valueRatio" : { Ratio },
  "valueSampledData" : { SampledData },
  "valueTime" : "<time>",
  "valueDateTime" : "<dateTime>",
  "valuePeriod" : { Period },
  "valueAttachment" : { Attachment },
  "valueReference" : { Reference(MolecularSequence) },
  "dataAbsentReason" : { CodeableConcept }, // I Why the result is missing
  "interpretation" : [{ CodeableConcept }], // High, low, normal, etc
  "note" : [{ Annotation }], // Comments about the observation
  "bodySite" : { CodeableConcept }, // I Observed body part
  "bodyStructure" : { Reference(BodyStructure) }, // I Observed body structure
  "method" : { CodeableConcept }, // How it was done
  "specimen" : { Reference(Group|Specimen) }, // Specimen used for this observation
  "device" : { Reference(Device|DeviceMetric) }, // A reference to the device that generates the measurements or the device settings for the device
  "referenceRange" : [{ // Provides guide for interpretation
    "low" : { Quantity(SimpleQuantity) }, // I Low Range, if relevant
    "high" : { Quantity(SimpleQuantity) }, // I High Range, if relevant
    "normalValue" : { CodeableConcept }, // Normal value, if relevant
    "type" : { CodeableConcept }, // Reference range qualifier
    "appliesTo" : [{ CodeableConcept }], // Reference range population
    "age" : { Range }, // Applicable age range, if relevant
    "text" : "<markdown>" // I Text based reference range in an observation
  }],
  "hasMember" : [{ Reference(MolecularSequence|Observation|
   QuestionnaireResponse) }], // Related resource that belongs to the Observation group
  "derivedFrom" : [{ Reference(DocumentReference|GenomicStudy|ImagingSelection|
   ImagingStudy|MolecularSequence|Observation|QuestionnaireResponse) }], // Related resource from which the observation is made
  "component" : [{ // I Component results
    "code" : { CodeableConcept }, // I R!  Type of component observation (code / type)
    // value[x]: Actual component result. One of these 13:
    "valueQuantity" : { Quantity },
    "valueCodeableConcept" : { CodeableConcept },
    "valueString" : "<string>",
    "valueBoolean" : <boolean>,
    "valueInteger" : <integer>,
    "valueRange" : { Range },
    "valueRatio" : { Ratio },
    "valueSampledData" : { SampledData },
    "valueTime" : "<time>",
    "valueDateTime" : "<dateTime>",
    "valuePeriod" : { Period },
    "valueAttachment" : { Attachment },
    "valueReference" : { Reference(MolecularSequence) },
    "dataAbsentReason" : { CodeableConcept }, // Why the component result is missing
    "interpretation" : [{ CodeableConcept }], // High, low, normal, etc
    "referenceRange" : [{ Content as for Observation.referenceRange }] // Provides guide for interpretation of component result
  }]
}
```