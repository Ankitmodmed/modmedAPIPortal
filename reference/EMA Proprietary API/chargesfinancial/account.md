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
Base profile: [https://www.hl7.org/fhir/account.html](https://www.hl7.org/fhir/account.html)

Common use cases include:

* Find outstanding balances for a Patient

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
        GUID for the Account
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        Account.subject refers to the Patient. It is a FHIR Reference object. [http://www.hl7.org/fhir/references.html#Reference](http://www.hl7.org/fhir/references.html#Reference)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        guarantor
      </td>

      <td style={{ textAlign: "left" }}>
        party will reference Patient if the Guarantor is set to SELF\
        party will reference RelatedPerson if Guarantor is someone else
      </td>
    </tr>
  </tbody>
</Table>

The following extensions to the Account resource have been created and are supported in order to support the desired functionality:

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
        outstandingBalance
      </td>

      <td style={{ textAlign: "left" }}>
        Data Type = Money -\
        [http://www.hl7.org/fhir/datatypes.html#Money](http://www.hl7.org/fhir/datatypes.html#Money)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        unusedFunds
      </td>

      <td style={{ textAlign: "left" }}>
        Data Type = Money -\
        [http://www.hl7.org/fhir/datatypes.html#Money](http://www.hl7.org/fhir/datatypes.html#Money)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        businessUnitId
      </td>

      <td style={{ textAlign: "left" }}>
        Unique identifier for the practice which must be included in all posted PaymentReconciliation objects
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        businessUnitName
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* Account SEARCH
