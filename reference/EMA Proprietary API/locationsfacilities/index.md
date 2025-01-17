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
Base Profile: [https://www.hl7.org/fhir/location.html](https://www.hl7.org/fhir/location.html)

Common use cases include:

* Find the Locations of a Practice
* Find the identifiers of Locations
* Find the BusinessUnit for a Location
* Search for a Location by name

The following attributes are supported:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Field Name
      </th>

      <th style={{ textAlign: "left" }}>
        Notes
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        id
      </td>

      <td style={{ textAlign: "left" }}>
        The MMI-specific unique identifier for the location
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        Other identifiers for the Location:

        * BusinessUnitId (for when the practice is using ModMed Practice Management System)
        * PMSID (additional identifier for the location used in HL7 interfaces and sometimes needs to be used in conjunction with the API)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        active|inactive
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        Name of the practice (location)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        address
      </td>

      <td style={{ textAlign: "left" }}>
        Address of the location
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* Location READ
* Location SEARCH