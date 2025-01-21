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

The CareTeam resource in FHIR represents a group of people and/or organizations who plan to participate or who are participating in the coordination and delivery of care for a patient.\
The CareTeam endpoint is used to interact with CareTeam resources over RESTful APIs. It allows you to create, read, update, and delete care teams.

### Here are some key elements of the CareTeam resource:

* **Identifier**: Unique identifier for the CareTeam.
* **Status**: Indicates the current state of the care team (e.g., active, suspended).
* **Category**: Type of team, such as multidisciplinary.
* **Name**: Name of the care team.
* **Subject**: The patient or group the care team is for.
* **Period**: The time period the care team covers.
* **Participant**: Members of the care team with their roles, contact details, and statuses.

<br />

New content:

The Care Team includes all the people and organizations who plan to participate in the coordination and delivery of care for a patient.

Read more from : [https://hl7.org/fhir/R4/careteam.html](https://hl7.org/fhir/R4/careteam.html)

<br />

Sample Response Object:

```Text json
{
  "resourceType": "CareTeam",
  "id": "example-careteam",
  "status": "active",
  "name": "General Practice Care Team",
  "subject": {
    "reference": "Patient/example"
  },
  "period": {
    "start": "2021-01-01",
    "end": "2022-01-01"
  },
  "participant": [
    {
      "role": [
        {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/participant-role",
              "code": "practitioner",
              "display": "Practitioner"
            }
          ]
        }
      ],
      "member": {
        "reference": "Practitioner/1",
        "display": "Dr. John Smith"
      },
      "onBehalfOf": {
        "reference": "Organization/1",
        "display": "Healthcare Organization"
      },
      "period": {
        "start": "2021-01-01"
      }
    },
    {
      "role": [
        {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/participant-role",
              "code": "nurse",
              "display": "Nurse"
            }
          ]
        }
      ],
      "member": {
        "reference": "Practitioner/2",
        "display": "Nurse Ellen"
      },
      "period": {
        "start": "2021-03-01"
      }
    }
  ]
}
```
```json new json
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