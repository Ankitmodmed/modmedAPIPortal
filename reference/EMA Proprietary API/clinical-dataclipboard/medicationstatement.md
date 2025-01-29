---
title: Medication Statement
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
Base Profile: https:[www.hl7.org/fhir/medicationstatement.html](http://www.hl7.org/fhir/medicationstatement.html)

Common use cases include:

* Find all Medications for a Patient
* Add a Medication to a Patient’s record
* Update a Medication status in a Patient’s record

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

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        active | completed | entered-in-error | intended | stopped | on-hold | unknown | not-taken

        Active and Stopped are the only statuses which our product currently supports. Any status other than stopped will be defaulted to Active in our system.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        medicationCodeableConcept
      </td>

      <td style={{ textAlign: "left" }}>
        system: rxnorm
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        reference to patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        effectivePeriod

        -start\
        -end
      </td>

      <td style={{ textAlign: "left" }}>
        date/time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        informationSource
      </td>

      <td style={{ textAlign: "left" }}>
        reference to Practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        dosage

        -route\
        -doseAndRate
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reasonCode

        -ICD Code\
        -DisplayName
        -Text
      </td>

      <td style={{ textAlign: "left" }}>
        ICD-10 (ICD-9 for older diagnoses) - Note: this will only appear if the medication was prescribed in EMA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        note

        -sig\
        -side effects
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

<br />

The Following Operations are supported:

* MedicationStatement READ
* MedicationStatement SEARCH
* MedicationStatement CREATE
* MedicationStatement UPDATE

### MedicationStatement CREATE

Note that Medications added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

The following attributes are supported with required fields marked with \*:

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
        status\*
      </td>

      <td style={{ textAlign: "left" }}>
        will default to active if not passed in
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject\*
      </td>

      <td style={{ textAlign: "left" }}>
        patient reference
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        medicationCodeableConcept\*
      </td>

      <td style={{ textAlign: "left" }}>
        RxNorm is supported as a code at this time.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        effectivePeriod

        -start
        -end
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        dosage

        -route\
        -doseAndRate
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

<br />

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
        status
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        effectivePeriod

        -end
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>