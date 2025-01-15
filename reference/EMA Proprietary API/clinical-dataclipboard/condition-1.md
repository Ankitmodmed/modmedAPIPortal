---
title: Condition
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
Base profile: &lt;https://www.hl7.org/fhir/condition.html&gt;

Common use cases include:

- Find all Conditions for a Patient
- Add a Condition to a Patient’s record
- Update a Condition’s status

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "clinicalStatus",
    "0-1": "Active, Inactive, Resolved",
    "1-0": "subject",
    "1-1": "Reference to Patient",
    "2-0": "code",
    "2-1": "ICD-9, ICD-10, SNOMED Name",
    "3-0": "onset",
    "3-1": "startdate/enddate",
    "4-0": "recordedDate",
    "4-1": "Date Recorded",
    "5-0": "category",
    "5-1": "Problem Type:  \nProblem|Condition|Diagnosis|Symptom|Finding|Complaint|Functional Limitation|Health Status"
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

- Condition READ
- Condition SEARCH
- Condition CREATE
- Condition UPDATE

***

### Condition CREATE

Note that Conditions added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

The following attributes are required for a CREATE:

| Field Name       | Notes                      |
| :--------------- | :------------------------- |
| \*clinicalStatus | Active, Inactive, Resolved |
| \*subject        | Reference to Patient       |
| \*code           | ICD-9, ICD-10, SNOMED Name |

***

### Condition UPDATE

Note that Conditions added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

For the purposes of clarity, the following fields are immutable:

| Field Name     | Notes |
| :------------- | :---- |
| subject\*      |       |
| code\*         |       |
| recordedDate\* |       |

For the purposes of clarity, the following fields are supported for UPDATE:

| Field Name     | Notes |
| :------------- | :---- |
| abatement      |       |
| clinicalStatus |       |
| category       |       |