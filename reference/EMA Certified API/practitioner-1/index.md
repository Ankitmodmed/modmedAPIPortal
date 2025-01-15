---
title: Practitioner
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-practitioner](http://hl7.org/fhir/us/core/StructureDefinition/us-core-practitioner)

The FHIR (Fast Healthcare Interoperability Resources) Practitioner resource is used to represent a healthcare practitioner, such as a doctor, nurse, or pharmacist, in a standard format that can be easily shared and understood across different healthcare systems.

## Key Components of the Practitioner Resource

1. **id**: A unique identifier for the practitioner.
2. **identifier**: Formal identifier(s) for the practitioner that can be used to identify the practitioner globally.
3. **active**: Indicates whether the practitioner is active.
4. **name**: The name of the practitioner, including family name, first name, and other name parts.
5. **telecom**: Contact details such as phone number, email address, etc.
6. **address**: The address details of the practitioner.
7. **gender**: The gender of the practitioner.
8. **birthDate**: The birth date of the practitioner.
9. **qualification**: The qualifications/certifications of the practitioner.
10. **communication**: A list of languages the practitioner can communicate in, with proficiency details.

**Sample Response Object:**

```Text json
{
  "resourceType": "Practitioner",
  "id": "example",
  "identifier": [
    {
      "system": "http://hospital.smarthealthit.org",
      "value": "12345"
    }
  ],
  "active": true,
  "name": [
    {
      "family": "Jones",
      "given": ["John", "Adam"],
      "prefix": ["Dr."]
    }
  ],
  "telecom": [
    {
      "system": "phone",
      "value": "555-555-1000",
      "use": "work"
    },
    {
      "system": "email",
      "value": "j.jones@hospital.org",
      "use": "work"
    }
  ],
  "address": [
    {
      "use": "work",
      "line": ["123 Healthcare Blvd"],
      "city": "Metro City",
      "state": "NY",
      "postalCode": "10001"
    }
  ],
  "gender": "male",
  "birthDate": "1970-01-01",
  "qualification": [
    {
      "identifier": [
        {
          "system": "http://example.org/qualifications",
          "value": "12345"
        }
      ],
      "code": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/v2-0360/2.7",
            "code": "MD",
            "display": "Doctor of Medicine"
          }
        ],
        "text": "Doctor of Medicine"
      },
      "period": {
        "start": "2000-01-01"
      },
      "issuer": {
        "display": "Example University"
      }
    }
  ],
  "communication": [
    {
      "language": {
        "coding": [
          {
            "system": "urn:ietf:bcp:47",
            "code": "en",
            "display": "English"
          }
        ],
        "text": "English"
      },
      "preferred": true
    }
  ]
}
```
