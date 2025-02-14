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

A Location includes both incidental locations (a place which is used for healthcare without prior designation or authorization) and dedicated, formally appointed locations. Locations may be private, public, mobile or fixed and scale from small freezers to full hospital buildings or parking garages.

Read more from: [https://hl7.org/fhir/R4/location.html](https://hl7.org/fhir/R4/location.html)

**Sample Response Object:**

```json json
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