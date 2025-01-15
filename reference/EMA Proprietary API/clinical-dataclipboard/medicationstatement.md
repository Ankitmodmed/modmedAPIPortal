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
Base Profile: https:/www.hl7.org/fhir/medicationstatement.html

Common use cases include:

- Find all Medications for a Patient
- Add a Medication to a Patient’s record
- Update a Medication status in a Patient’s record

The following attributes are supported:



The Following Operations are supported:

- MedicationStatement READ
- MedicationStatement SEARCH
- MedicationStatement CREATE
- MedicationStatement UPDATE


### MedicationStatement CREATE

Note that Medications added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

The following attributes are supported with required fields marked with \*:




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