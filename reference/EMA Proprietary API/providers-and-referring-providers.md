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
Base profile: <https://www.hl7.org/fhir/practitioner.html>

## Practitioner Types Supported by EMA

EMA supports two types of practitioners:

1. Standard Practitioners:  
   This includes any staff member within the practice. Typically, you can distinguish between a provider and other staff members by the presence of an NPI (National Provider Identifier) for providers.
2. Referring Providers:  
   These can be identified by querying the API with the following parameter:  
   `/Practitioner?type=ref`  
   This query will return all referring providers associated with the practice.

The following attributes are supported on ALL Practitioner calls:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The MMI-specific unique identifier for the practitioner",
    "1-0": "identifier",
    "1-1": "NPI:  \n<http://www.hl7.org/fhir/v2/0203/index.html#v2-0203-NPI>",
    "2-0": "active",
    "2-1": "true|false",
    "3-0": "name",
    "3-1": "- family\n- given",
    "4-0": "telecom",
    "4-1": "The various contact methods for the Practitioner."
  },
  "cols": 2,
  "rows": 5,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The following attributes are supported on Referring Practitioner calls:

| Field Name    | Notes                                 |
| :------------ | :------------------------------------ |
| qualification | The speciality of the provider.       |
| address       | The address of the Referring Provider |

**Common Use Cases:**

- Retrieve all staff members for a practice
- Find a specific staff member or provider
- Retrieve the NPI of a provider
- Find a specific referring provider
- Retrieve all referring providers within the practice

**The Following Operations are supported:**

- Practitioner READ
- Practitioner SEARCH
- Practitioner CREATE