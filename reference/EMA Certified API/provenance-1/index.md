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

FHIR (Fast Healthcare Interoperability Resources) Provenance is used to describe the origin or source of the information that is in a resource. This includes information about the entity or person involved in the creation, modification, or routing of the resource.

## Key Components of FHIR Provenance

1. **target**: List of resources that the Provenance is about.
2. **recorded**: The time when the activity was recorded.
3. **activity**: A coded representation of the type of activity performed (e.g., creation, modification).
4. **agent**: The individual(s), organization(s), or device(s) involved in the activity and their role.
5. **location**: The location where the activity occurred.
6. **entity**: The resources or objects used during the activity.
7. **signature**: Digital signatures for authenticity and integrity.

<br />

New content:

The Provenance resource tracks information about the activity that created, revised, deleted, or signed a version of a resource, describing the entities and agents involved. This information can be used to form assessments about its quality, reliability, trustworthiness, or to provide pointers for where to go to further investigate the origins of the resource and the information in it.

<br />

**Sample Response Object:**

```Text json
{
  "resourceType": "Provenance",
  "target": [
    {
      "reference": "Patient/12345"
    }
  ],
  "recorded": "2023-10-11T15:30:00Z",
  "agent": [
    {
      "type": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/provenance-agent-type",
            "code": "author",
            "display": "Author"
          }
        ]
      },
      "who": {
        "reference": "Practitioner/67890"
      }
    }
  ],
  "entity": [
    {
      "role": "source",
      "what": {
        "reference": "DocumentReference/abc123"
      }
    }
  ],
  "signature": [
    {
      "type": [
        {
          "system": "urn:iso-astm:E1762-95:2013",
          "code": "1.2.840.10065.1.12.1.1",
          "display": "Author's Signature"
        }
      ],
      "when": "2023-10-11T15:30:00Z",
      "who": {
        "reference": "Practitioner/67890"
      }
    }
  ]
}
```
```json new json
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