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

<br />

New content:

Practitioner covers all individuals who are engaged in the healthcare process and healthcare-related services as part of their formal responsibilities and this Resource is used for attribution of activities and responsibilities to these individuals.

Read more from: [https://hl7.org/fhir/R4/practitioner.html](https://hl7.org/fhir/R4/practitioner.html)

<br />

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
```json new json
{
  "resourceType" : "Practitioner",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // An identifier for the person as this agent
  "active" : <boolean>, // Whether this practitioner's record is in active use
  "name" : [{ HumanName }], // The name(s) associated with the practitioner
  "telecom" : [{ ContactPoint }], // A contact detail for the practitioner (that apply to all roles)
  "address" : [{ Address }], // Address(es) of the practitioner that are not role specific (typically home address)
  "gender" : "<code>", // male | female | other | unknown
  "birthDate" : "<date>", // The date  on which the practitioner was born
  "photo" : [{ Attachment }], // Image of the person
  "qualification" : [{ // Certification, licenses, or training pertaining to the provision of care
    "identifier" : [{ Identifier }], // An identifier for this qualification for the practitioner
    "code" : { CodeableConcept }, // R!  Coded representation of the qualification
    "period" : { Period }, // Period during which the qualification is valid
    "issuer" : { Reference(Organization) } // Organization that regulates and issues the qualification
  }],
  "communication" : [{ CodeableConcept }] // A language the practitioner can use in patient communication
}
```