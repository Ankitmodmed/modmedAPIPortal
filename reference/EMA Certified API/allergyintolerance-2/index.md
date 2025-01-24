---
title: AllergyIntolerance
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

AllergyIntolerance resource is used to provide a single place within the health record to document a range of clinical statements about adverse reactions to substances/products.

Read more from: [https://hl7.org/fhir/R4/allergyintolerance.html](https://hl7.org/fhir/R4/allergyintolerance.html)

<br />

**Sample Response Object:**

```Text json
{
  "resourceType" : "AllergyIntolerance",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External ids for this item
  "clinicalStatus" : { CodeableConcept }, // C? active | inactive | resolved
  "verificationStatus" : { CodeableConcept }, // C? unconfirmed | confirmed | refuted | entered-in-error
  "type" : "<code>", // allergy | intolerance - Underlying mechanism (if known)
  "category" : ["<code>"], // food | medication | environment | biologic
  "criticality" : "<code>", // low | high | unable-to-assess
  "code" : { CodeableConcept }, // Code that identifies the allergy or intolerance
  "patient" : { Reference(Patient) }, // R!  Who the sensitivity is for
  "encounter" : { Reference(Encounter) }, // Encounter when the allergy or intolerance was asserted
  // onset[x]: When allergy or intolerance was identified. One of these 5:
  "onsetDateTime" : "<dateTime>",
  "onsetAge" : { Age },
  "onsetPeriod" : { Period },
  "onsetRange" : { Range },
  "onsetString" : "<string>",
  "recordedDate" : "<dateTime>", // Date first version of the resource instance was recorded
  "recorder" : { Reference(Practitioner|PractitionerRole|Patient|
   RelatedPerson) }, // Who recorded the sensitivity
  "asserter" : { Reference(Patient|RelatedPerson|Practitioner|
   PractitionerRole) }, // Source of the information about the allergy
  "lastOccurrence" : "<dateTime>", // Date(/time) of last known occurrence of a reaction
  "note" : [{ Annotation }], // Additional text not captured in other fields
  "reaction" : [{ // Adverse Reaction Events linked to exposure to substance
    "substance" : { CodeableConcept }, // Specific substance or pharmaceutical product considered to be responsible for event
    "manifestation" : [{ CodeableConcept }], // R!  Clinical symptoms/signs associated with the Event
    "description" : "<string>", // Description of the event as a whole
    "onset" : "<dateTime>", // Date(/time) when manifestations showed
    "severity" : "<code>", // mild | moderate | severe (of event as a whole)
    "exposureRoute" : { CodeableConcept }, // How the subject was exposed to the substance
    "note" : [{ Annotation }] // Text about event not captured in other fields
  }]
}
```