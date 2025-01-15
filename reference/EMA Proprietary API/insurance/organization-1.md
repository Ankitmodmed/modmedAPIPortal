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
Currently the ‘Organization’ resource can only be used to query two different data sets. It can be used to find Payers in the ModMed Practice Management system. It can also be used to find Referring Institutions within EMA/MMPM. We will be expanding on the Organization resource to include other types of Organizations in the future, so if you are looking for additional functionality, be sure to check back.

The following attributes are supported in cases that the Organization is a Payer:

| Field Name | Notes                                              |
| :--------- | :------------------------------------------------- |
| id         | ID of the Organization                             |
| identifier | payerID for Payers, npi for Referring Institutions |
| active     | true\|false                                        |
| type       | “pay” or “prov”                                    |
| name       | Name of the Payer or Referring Institution         |

The Following additional attributes are supported additionally for Organizations that are Referring Institutions.

| Field Name | Notes                                                                                       |
| :--------- | :------------------------------------------------------------------------------------------ |
| telecom    | work , fax, mobile phone numbers, email, hisp address (Health Information Service Provider) |
| address    | office address                                                                              |

The Following Operations are supported:

* Organization READ
* Organization SEARCH
* Organization CREATE(supported only for Referring Institutions)

### Organization CREATE

The following attributes are required:

<br />

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
        true
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        code = ‘prov’
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        address
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

The following attributes are optional to send in:

| Field Name | Notes                                           |
| :--------- | :---------------------------------------------- |
| telecom    | email, alternate email, work phone, fax, mobile |
