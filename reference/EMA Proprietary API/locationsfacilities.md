---
title: Locations/Facilities
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
Base Profile: <https://www.hl7.org/fhir/location.html>

Common use cases include:

- Find the Locations of a Practice
- Find the identifiers of Locations
- Find the BusinessUnit for a Location
- Search for a Location by name

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The MMI-specific unique identifier for the location",
    "1-0": "identifier",
    "1-1": "Other identifiers for the Location:    \n  \n- BusinessUnitId (for when the practice is using Modernizing Medicine Practice Management System) \n- PMSID (additional identifier for the location used in HL7 interfaces and sometimes needs to be used in conjunction with the API)",
    "2-0": "status",
    "2-1": "active|inactive",
    "3-0": "name",
    "3-1": "Name of the practice (location)",
    "4-0": "address",
    "4-1": "Address of the location"
  },
  "cols": 2,
  "rows": 5,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- Location READ
- Location SEARCH