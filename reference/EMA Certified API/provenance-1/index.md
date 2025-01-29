---
title: Provenance
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-provenance](http://hl7.org/fhir/us/core/StructureDefinition/us-core-provenance)

The Provenance resource tracks information about the activity that created, revised, deleted, or signed a version of a resource, describing the entities and agents involved. This information can be used to form assessments about its quality, reliability, trustworthiness, or to provide pointers for where to go to further investigate the origins of the resource and the information in it.

Read more on: [https://hl7.org/fhir/R4/provenance.html](https://hl7.org/fhir/R4/provenance.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "Provenance",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "target" : [{ Reference(Any) }], // R!  Target Reference(s) (usually version specific)
  // occurred[x]: When the activity occurred. One of these 2:
  "occurredPeriod" : { Period },
  "occurredDateTime" : "<dateTime>",
  "recorded" : "<instant>", // R!  When the activity was recorded / updated
  "policy" : ["<uri>"], // Policy or plan the activity was defined by
  "location" : { Reference(Location) }, // Where the activity occurred, if relevant
  "reason" : [{ CodeableConcept }], // Reason the activity is occurring
  "activity" : { CodeableConcept }, // Activity that occurred
  "agent" : [{ // R!  Actor involved
    "type" : { CodeableConcept }, // How the agent participated
    "role" : [{ CodeableConcept }], // What the agents role was
    "who" : { Reference(Practitioner|PractitionerRole|RelatedPerson|Patient|
    Device|Organization) }, // R!  Who participated
    "onBehalfOf" : { Reference(Practitioner|PractitionerRole|RelatedPerson|
    Patient|Device|Organization) } // Who the agent is representing
  }],
  "entity" : [{ // An entity used in this activity
    "role" : "<code>", // R!  derivation | revision | quotation | source | removal
    "what" : { Reference(Any) }, // R!  Identity of entity
    "agent" : [{ Content as for Provenance.agent }] // Entity is attributed to this agent
  }],
  "signature" : [{ Signature }] // Signature on target
}
```

In this sample response:

* The `target` refers to a Patient resource.
* The `recorded` time is provided.
* The `agent` specifies the author (a practitioner).
* The `entity` specifies a DocumentReference resource used as a source.
* A `signature` is included to ensure authenticity.