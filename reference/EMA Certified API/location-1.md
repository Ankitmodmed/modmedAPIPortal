---
title: Location
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
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-location>

The Location resource is used to describe a physical location where healthcare services are provided.  
Here is an overview of key components of the FHIR Location resource, along with a sample response:

### Key Components:

1. **identifier**: A unique identifier for the location (e.g., a code assigned by the healthcare organization).
2. **status**: The operational status of the location (e.g., active, suspended).
3. **name**: The name of the location (e.g., "Main Hospital").
4. **description**: Additional description about the location.
5. **mode**: Indicates whether the location is a physical location or a set of locations (e.g., instance, kind).
6. **type**: The type of location (e.g., hospital, clinic) coded with values from a standard set of location types.
7. **telecom**: Contact details for the location (e.g., phone number, email).
8. **address**: The physical address of the location.
9. **position**: The geographical coordinates (latitude, longitude, altitude) of the location.
10. **managingOrganization**: The organization that is responsible for managing the location.
11. **partOf**: The location that this location is a part of.
12. **endpoint**: Associated endpoints for the location.

**Sample Response Object:**

```Text json
{
  "resourceType": "Location",
  "id": "example",
  "identifier": [
    {
      "use": "official",
      "value": "12345"
    }
  ],
  "status": "active",
  "name": "Main Hospital",
  "description": "Main campus of the healthcare organization",
  "mode": "instance",
  "type": [
    {
      "coding": [
        {
          "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
          "code": "HOSP",
          "display": "Hospital"
        }
      ]
    }
  ],
  "telecom": [
    {
      "system": "phone",
      "value": "(555) 123-4567",
      "use": "work"
    }
  ],
  "address": {
    "use": "work",
    "type": "both",
    "text": "123 Main St, Anytown, USA",
    "line": [
      "123 Main St"
    ],
    "city": "Anytown",
    "state": "CA",
    "postalCode": "94301",
    "country": "USA"
  },
  "position": {
    "longitude": -122.406417,
    "latitude": 37.785834,
    "altitude": 30
  },
  "managingOrganization": {
    "reference": "Organization/1",
    "display": "Healthcare Organization"
  },
  "partOf": {
    "reference": "Location/2",
    "display": "Main Building"
  },
  "endpoint": [
    {
      "reference": "Endpoint/example",
      "display": "FHIR Endpoint"
    }
  ]
}
```