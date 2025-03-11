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
Base Profile: [https://www.hl7.org/fhir/familymemberhistory.html](https://www.hl7.org/fhir/familymemberhistory.html)

Common use cases include:

* Find the Family History of a Patient

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
        patient
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        Supported Statuses:    

        * Active = partial  
        * Completed = completed  
        * Prior History No longer Active = health-unknown
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        relationship
      </td>

      <td style={{ textAlign: "left" }}>
        * Mother : 72705000  
        * Father : 66839005  
        * Sister : 27733009  
        * Brother : 70924004  
        * Daughter : 66089001  
        * Son : 65616008  
        * Uncle : 38048003  
        * Aunt : 25211005  
        * Nephew : 83559000  
        * Niece : 34581001  
        * Grandmother : 113157001  
        * Grandfather : 34871008  
        * Granddaughter : 44181008  
        * Grandson : 70578009  
        * Other : 35359004
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        date
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        note
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        condition
      </td>

      <td style={{ textAlign: "left" }}>
        code + name
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* FamilyMemberHistory READ
* FamilyMemberHistory SEARCH

***

### FamilyMemberHistory SEARCH

The FamilyMemberHistory resource is searchable by the following parameters:

| Name    | Type      | Description |
| :------ | :-------- | :---------- |
| patient | reference | Patient id  |