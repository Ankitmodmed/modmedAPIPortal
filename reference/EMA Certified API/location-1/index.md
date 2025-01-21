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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-location](http://hl7.org/fhir/us/core/StructureDefinition/us-core-location)

The Location resource is used to describe a physical location where healthcare services are provided.\
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

<br />

New content:

A Location includes both incidental locations (a place which is used for healthcare without prior designation or authorization) and dedicated, formally appointed locations. Locations may be private, public, mobile or fixed and scale from small freezers to full hospital buildings or parking garages.

Read more from: [https://hl7.org/fhir/R4/location.html](https://hl7.org/fhir/R4/location.html)

<br />

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
```json new json
{
  "resourceType" : "Location",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Unique code or number identifying the location to its users
  "status" : "<code>", // active | suspended | inactive
  "operationalStatus" : { Coding }, // The operational status of the location (typically only for a bed/room)
  "name" : "<string>", // Name of the location as used by humans
  "alias" : ["<string>"], // A list of alternate names that the location is known as, or was known as, in the past
  "description" : "<string>", // Additional details about the location that could be displayed as further information to identify the location beyond its name
  "mode" : "<code>", // instance | kind
  "type" : [{ CodeableConcept }], // Type of function performed
  "telecom" : [{ ContactPoint }], // Contact details of the location
  "address" : { Address }, // Physical location
  "physicalType" : { CodeableConcept }, // Physical form of the location
  "position" : { // The absolute geographic location
    "longitude" : <decimal>, // R!  Longitude with WGS84 datum
    "latitude" : <decimal>, // R!  Latitude with WGS84 datum
    "altitude" : <decimal> // Altitude with WGS84 datum
  },
  "managingOrganization" : { Reference(Organization) }, // Organization responsible for provisioning and upkeep
  "partOf" : { Reference(Location) }, // Another Location this one is physically a part of
  "hoursOfOperation" : [{ // What days/times during a week is this location usually open
    "daysOfWeek" : ["<code>"], // mon | tue | wed | thu | fri | sat | sun
    "allDay" : <boolean>, // The Location is open all day
    "openingTime" : "<time>", // Time that the Location opens
    "closingTime" : "<time>" // Time that the Location closes
  }],
  "availabilityExceptions" : "<string>", // Description of availability exceptions
  "endpoint" : [{ Reference(Endpoint) }] // Technical endpoints providing access to services operated for the location
}
```