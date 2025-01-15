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
