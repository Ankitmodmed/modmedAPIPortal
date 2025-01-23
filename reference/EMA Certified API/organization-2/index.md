---
title: Organization
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-organization](http://hl7.org/fhir/us/core/StructureDefinition/us-core-organization)

The Organization resource in FHIR represents a group, such as a healthcare provider or insurance company. The endpoint for an organization typically retrieves detailed information about these entities.

## Key elements in the response

* **resourceType:** Indicates the type of resource, which is Organization.
* **id:** A unique identifier for the organization resource.
* **identifier:** An array of identifiers, each with a system and value.
* **active:** Indicates whether the organization is currently active.
* **type:** Describes the type of organization, with coding details.
* **name:** The official name of the organization.
* **telecom:** Contact information, including phone and email.
* **address:** Physical address of the organization, typically including lines, city, state, postal code, and country.

New content:

The Organization resource is used for collections of people that have come together to achieve an objective.It often exists as a hierarchy of organization resources, using the part-of property to provide the association of the child to its parent organization.

Read more from: [https://hl7.org/fhir/R4/organization.html](https://hl7.org/fhir/R4/organization.html)

**Sample Response Object:**

```Text json
{
    "resourceType": "Organization",
    "id": "example",
    "identifier": [
        {
            "system": "http://hospital.smarthealth.it/cpo",
            "value": "12345"
        }
    ],
    "active": true,
    "type": [
        {
            "coding": [
                {
                    "system": "http://terminology.hl7.org/CodeSystem/organization-type",
                    "code": "prov",
                    "display": "Healthcare Provider"
                }
            ]
        }
    ],
    "name": "Health System",
    "telecom": [
        {
            "system": "phone",
            "value": "+1-800-555-1234",
            "use": "work"
        },
        {
            "system": "email",
            "value": "contact@healthsystem.org"
        }
    ],
    "address": [
        {
            "use": "work",
            "line": [
                "1234 Health St"
            ],
            "city": "Healthy City",
            "state": "HS",
            "postalCode": "12345",
            "country": "USA"
        }
    ]
}
```
```json new json
{
  "resourceType" : "Organization",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // C? Identifies this organization  across multiple systems
  "active" : <boolean>, // Whether the organization's record is still in active use
  "type" : [{ CodeableConcept }], // Kind of organization
  "name" : "<string>", // C? Name used for the organization
  "alias" : ["<string>"], // A list of alternate names that the organization is known as, or was known as in the past
  "telecom" : [{ ContactPoint }], // C? A contact detail for the organization
  "address" : [{ Address }], // C? An address for the organization
  "partOf" : { Reference(Organization) }, // The organization of which this organization forms a part
  "contact" : [{ // Contact for the organization for a certain purpose
    "purpose" : { CodeableConcept }, // The type of contact
    "name" : { HumanName }, // A name associated with the contact
    "telecom" : [{ ContactPoint }], // Contact details (telephone, email, etc.)  for a contact
    "address" : { Address } // Visiting or postal addresses for the contact
  }],
  "endpoint" : [{ Reference(Endpoint) }] // Technical endpoints providing access to services operated for the organization
}
```