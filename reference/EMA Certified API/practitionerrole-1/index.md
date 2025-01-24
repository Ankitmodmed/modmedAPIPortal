---
title: PractitionerRole
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-practitionerrole](http://hl7.org/fhir/us/core/StructureDefinition/us-core-practitionerrole)

The PractitionerRole resource in FHIR refers to the roles a practitioner plays at an organization.

## Key Components of PractitionerRole

1. **Practitioner**: Reference to the Practitioner resource (the individual performing the role).
2. **Organization**: Reference to the Organization resource associated with the practitioner.
3. **Code**: The role or specialty of the practitioner (e.g., Cardiologist, Oncologist).
4. **Specialty**: Specific specialties of the practitioner within the healthcare services conferred.
5. **Location**: Locations where the practitioner provides service(s).
6. **HealthcareService**: Details of the healthcare services offered.
7. **Telecom**: Contact details (e.g., phone, email).
8. **AvailableTime**: Timings when the practitioner is available.
9. **NotAvailable**: Specific periods when the practitioner is not available.
10. **Endpoint**: Technical endpoints for direct or automated communications.

<br />

New content:

PractitionerRole covers the recording of the location and types of services that Practitioners are able to provide for an organization.

Read more from: [https://www.hl7.org/implement/standards/fhir/R4/practitionerrole.html](https://www.hl7.org/implement/standards/fhir/R4/practitionerrole.html)

<br />

**Sample Response Object:**

```Text json
{
  "resourceType": "PractitionerRole",
  "id": "example",
  "practitioner": {
    "reference": "Practitioner/example",
    "display": "Dr. John Doe"
  },
  "organization": {
    "reference": "Organization/example",
    "display": "Healthcare Organization XYZ"
  },
  "code": [
    {
      "coding": [
        {
          "system": "http://terminology.hl7.org/CodeSystem/practitioner-role",
          "code": "doctor",
          "display": "Doctor"
        }
      ],
      "text": "Primary Care Physician"
    }
  ],
  "specialty": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "408443003",
          "display": "General practice"
        }
      ],
      "text": "General Practitioner"
    }
  ],
  "location": [
    {
      "reference": "Location/example",
      "display": "Main Clinic"
    }
  ],
  "telecom": [
    {
      "system": "phone",
      "value": "555-555-1003",
      "use": "work"
    },
    {
      "system": "email",
      "value": "johndoe@example.com",
      "use": "work"
    }
  ],
  "availableTime": [
    {
      "daysOfWeek": ["mon", "tue", "wed"],
      "availableStartTime": "09:00:00",
      "availableEndTime": "17:00:00"
    }
  ],
  "notAvailable": [
    {
      "description": "Annual leave",
      "during": {
        "start": "2023-12-25",
        "end": "2023-12-31"
      }
    }
  ],
  "endpoint": [
    {
      "reference": "Endpoint/example",
      "display": "FHIR Server API Endpoint"
    }
  ]
}
```
```json new json
{
  "resourceType" : "PractitionerRole",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business Identifiers that are specific to a role/location
  "active" : <boolean>, // Whether this practitioner role record is in active use
  "period" : { Period }, // The period during which the practitioner is authorized to perform in these role(s)
  "practitioner" : { Reference(Practitioner) }, // Practitioner that is able to provide the defined services for the organization
  "organization" : { Reference(Organization) }, // Organization where the roles are available
  "code" : [{ CodeableConcept }], // Roles which this practitioner may perform
  "specialty" : [{ CodeableConcept }], // Specific specialty of the practitioner
  "location" : [{ Reference(Location) }], // The location(s) at which this practitioner provides care
  "healthcareService" : [{ Reference(HealthcareService) }], // The list of healthcare services that this worker provides for this role's Organization/Location(s)
  "telecom" : [{ ContactPoint }], // Contact details that are specific to the role/location/service
  "availableTime" : [{ // Times the Service Site is available
    "daysOfWeek" : ["<code>"], // mon | tue | wed | thu | fri | sat | sun
    "allDay" : <boolean>, // Always available? e.g. 24 hour service
    "availableStartTime" : "<time>", // Opening time of day (ignored if allDay = true)
    "availableEndTime" : "<time>" // Closing time of day (ignored if allDay = true)
  }],
  "notAvailable" : [{ // Not available during this time due to provided reason
    "description" : "<string>", // R!  Reason presented to the user explaining why time not available
    "during" : { Period } // Service not available from this date
  }],
  "availabilityExceptions" : "<string>", // Description of availability exceptions
  "endpoint" : [{ Reference(Endpoint) }] // Technical endpoints providing access to services operated for the practitioner with this role
}
```