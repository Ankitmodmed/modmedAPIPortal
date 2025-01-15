---
title: Account
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
Base profile: <https://www.hl7.org/fhir/account.html>

Common use cases include:

- Find outstanding balances for a Patient

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "GUID for the Account",
    "1-0": "subject",
    "1-1": "Account.subject refers to the Patient. It is a FHIR Reference object. <http://www.hl7.org/fhir/references.html#Reference>",
    "2-0": "guarantor",
    "2-1": "party will reference Patient if the Guarantor is set to SELF  \nparty will reference RelatedPerson if Guarantor is someone else"
  },
  "cols": 2,
  "rows": 3,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The following extensions to the Account resource have been created and are supported in order to support the desired functionality:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "outstandingBalance",
    "0-1": "Data Type = Money -  \n<http://www.hl7.org/fhir/datatypes.html#Money>",
    "1-0": "unusedFunds",
    "1-1": "Data Type = Money -  \n<http://www.hl7.org/fhir/datatypes.html#Money>",
    "2-0": "businessUnitId",
    "2-1": "Unique identifier for the practice which must be included in all posted PaymentReconciliation objects",
    "3-0": "businessUnitName",
    "3-1": ""
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- Account SEARCH