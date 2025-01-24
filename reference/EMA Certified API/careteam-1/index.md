---
title: CareTeam
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-careteam](http://hl7.org/fhir/us/core/StructureDefinition/us-core-careteam)

The Care Team includes all the people and organizations who plan to participate in the coordination and delivery of care for a patient.

Read more from : [https://hl7.org/fhir/R4/careteam.html](https://hl7.org/fhir/R4/careteam.html)

Sample Response Object:

```json json
{
  "resourceType" : "CareTeam",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External Ids for this team
  "status" : "<code>", // proposed | active | suspended | inactive | entered-in-error
  "category" : [{ CodeableConcept }], // Type of team
  "name" : "<string>", // Name of the team, such as crisis assessment team
  "subject" : { Reference(Patient|Group) }, // Who care team is for
  "encounter" : { Reference(Encounter) }, // Encounter created as part of
  "period" : { Period }, // Time period team covers
  "participant" : [{ // C? Members of the team
    "role" : [{ CodeableConcept }], // Type of involvement
    "member" : { Reference(Practitioner|PractitionerRole|RelatedPerson|Patient|
    Organization|CareTeam) }, // Who is involved
    "onBehalfOf" : { Reference(Organization) }, // Organization of the practitioner
    "period" : { Period } // Time period of participant
  }],
  "reasonCode" : [{ CodeableConcept }], // Why the care team exists
  "reasonReference" : [{ Reference(Condition) }], // Why the care team exists
  "managingOrganization" : [{ Reference(Organization) }], // Organization responsible for the care team
  "telecom" : [{ ContactPoint }], // A contact detail for the care team (that applies to all members)
  "note" : [{ Annotation }] // Comments made about the CareTeam
}
```