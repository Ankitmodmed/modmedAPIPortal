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
