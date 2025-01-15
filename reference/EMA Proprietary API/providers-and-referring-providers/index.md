---
title: Providers and Referring Providers
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
Base profile: [https://www.hl7.org/fhir/practitioner.html](https://www.hl7.org/fhir/practitioner.html)

## Practitioner Types Supported by EMA

EMA supports two types of practitioners:

1. Standard Practitioners:\
   This includes any staff member within the practice. Typically, you can distinguish between a provider and other staff members by the presence of an NPI (National Provider Identifier) for providers.
2. Referring Providers:\
   These can be identified by querying the API with the following parameter:\
   `/Practitioner?type=ref`\
   This query will return all referring providers associated with the practice.

The following attributes are supported on ALL Practitioner calls:

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
        The MMI-specific unique identifier for the practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        NPI:\
        [http://www.hl7.org/fhir/v2/0203/index.html#v2-0203-NPI](http://www.hl7.org/fhir/v2/0203/index.html#v2-0203-NPI)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        active
      </td>

      <td style={{ textAlign: "left" }}>
        true|false
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        * family
        * given
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        telecom
      </td>

      <td style={{ textAlign: "left" }}>
        The various contact methods for the Practitioner.
      </td>
    </tr>
  </tbody>
</Table>

The following attributes are supported on Referring Practitioner calls:

| Field Name    | Notes                                 |
| :------------ | :------------------------------------ |
| qualification | The speciality of the provider.       |
| address       | The address of the Referring Provider |

**Common Use Cases:**

* Retrieve all staff members for a practice
* Find a specific staff member or provider
* Retrieve the NPI of a provider
* Find a specific referring provider
* Retrieve all referring providers within the practice

**The Following Operations are supported:**

* Practitioner READ
* Practitioner SEARCH
* Practitioner CREATE
