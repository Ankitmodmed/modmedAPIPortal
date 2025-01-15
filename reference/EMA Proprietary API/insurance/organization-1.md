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

- Organization READ
- Organization SEARCH
- Organization CREATE(supported only for Referring Institutions)

### Organization CREATE

The following attributes are required:

<br />

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "identifier",
    "0-1": "NPI:  \n<http://www.hl7.org/fhir/v2/0203/index.html#v2-0203-NPI>",
    "1-0": "active",
    "1-1": "true",
    "2-0": "type",
    "2-1": "code = ‘prov’",
    "3-0": "name",
    "3-1": "",
    "4-0": "address",
    "4-1": ""
  },
  "cols": 2,
  "rows": 5,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The following attributes are optional to send in:

| Field Name | Notes                                           |
| :--------- | :---------------------------------------------- |
| telecom    | email, alternate email, work phone, fax, mobile |