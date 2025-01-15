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
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-careteam>

The CareTeam resource in FHIR represents a group of people and/or organizations who plan to participate or who are participating in the coordination and delivery of care for a patient.  
The CareTeam endpoint is used to interact with CareTeam resources over RESTful APIs. It allows you to create, read, update, and delete care teams.

### Here are some key elements of the CareTeam resource:

- **Identifier**: Unique identifier for the CareTeam.
- **Status**: Indicates the current state of the care team (e.g., active, suspended).
- **Category**: Type of team, such as multidisciplinary.
- **Name**: Name of the care team.
- **Subject**: The patient or group the care team is for.
- **Period**: The time period the care team covers.
- **Participant**: Members of the care team with their roles, contact details, and statuses.

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