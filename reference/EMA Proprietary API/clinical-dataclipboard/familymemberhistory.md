---
title: FamilyMemberHistory
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
Base Profile: <https://www.hl7.org/fhir/familymemberhistory.html>

Common use cases include:

- Find the Family History of a Patient

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "patient",
    "0-1": "reference",
    "1-0": "status",
    "1-1": "Supported Statuses:    \n  \n- Active = partial  \n- Completed = completed  \n- Prior History No longer Active = health-unknown",
    "2-0": "relationship",
    "2-1": "- Mother : 72705000  \n- Father : 66839005  \n- Sister : 27733009  \n- Brother : 70924004  \n- Daughter : 66089001  \n- Son : 65616008  \n- Uncle : 38048003  \n- Aunt : 25211005  \n- Nephew : 83559000  \n- Niece : 34581001  \n- Grandmother : 113157001  \n- Grandfather : 34871008  \n- Granddaughter : 44181008  \n- Grandson : 70578009  \n- Other : 35359004",
    "3-0": "date",
    "3-1": "datetime",
    "4-0": "note",
    "4-1": "string",
    "5-0": "condition",
    "5-1": "code + name"
  },
  "cols": 2,
  "rows": 6,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- FamilyMemberHistory READ
- FamilyMemberHistory SEARCH

***

### FamilyMemberHistory SEARCH

The FamilyMemberHistory resource is searchable by the following parameters:

| Name    | Type      | Description |
| :------ | :-------- | :---------- |
| patient | reference | Patient id  |