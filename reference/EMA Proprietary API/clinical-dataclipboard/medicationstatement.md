---
title: MedicationStatement
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
Base Profile: <https://www.hl7.org/fhir/medicationstatement.html>

Common use cases include:

- Find all Medications for a Patient
- Add a Medication to a Patient’s record
- Update a Medication status in a Patient’s record

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "",
    "1-0": "status",
    "1-1": "active | completed | entered-in-error | intended | stopped | on-hold | unknown | not-taken  \n  \nActive and Stopped are the only statuses which our product currently supports. Any status other than stopped will be defaulted to Active in our system.",
    "2-0": "medicationCodeableConcept",
    "2-1": "system: rxnorm",
    "3-0": "subject",
    "3-1": "reference to patient",
    "4-0": "effectivePeriod  \n  \n- start\n- end",
    "4-1": "date/time",
    "5-0": "informationSource",
    "5-1": "reference to Practitioner",
    "6-0": "dosage  \n  \n- route\n- doseAndRate",
    "6-1": "",
    "7-0": "reasonCode  \n  \n- ICD Code\n- DisplayName\n- Text",
    "7-1": "ICD-10 (ICD-9 for older diagnoses) - Note: this will only appear if the medication was prescribed in EMA",
    "8-0": "note  \n  \n- sig\n- side effects",
    "8-1": ""
  },
  "cols": 2,
  "rows": 9,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- MedicationStatement READ
- MedicationStatement SEARCH
- MedicationStatement CREATE
- MedicationStatement UPDATE

***

### MedicationStatement CREATE

Note that Medications added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

The following attributes are supported with required fields marked with \*:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "status\\*",
    "0-1": "will default to active if not passed in",
    "1-0": "subject\\*",
    "1-1": "patient reference",
    "2-0": "medicationCodeableConcept\\*",
    "2-1": "RxNorm is supported as a code at this time.",
    "3-0": "effectivePeriod  \n  \n- start\n- end",
    "3-1": "",
    "4-0": "dosage  \n  \n- route\n- doseAndRate",
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


***

### MedicationStatement UPDATE

Note that Medications added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

For the purposes of clarity, the following fields are immutable:

| Field Name                  | Notes |
| :-------------------------- | :---- |
| informationSource\*         |       |
| subject\*                   |       |
| medicationCodeableConcept\* |       |
| dosage\*                    |       |
| reasonCode\*                |       |
| note\*                      |       |

For the purposes of clarity, the following fields are supported for UPDATE:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "status",
    "0-1": "",
    "1-0": "effectivePeriod  \n  \n- end",
    "1-1": ""
  },
  "cols": 2,
  "rows": 2,
  "align": [
    "left",
    "left"
  ]
}
[/block]