---
title: RelatedPerson
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
Base profile: [https://www.hl7.org/fhir/relatedperson.html](https://www.hl7.org/fhir/relatedperson.html)

RelatedPersons typically have a personal relationship or non-healthcare-specific professional relationship to the patient. A RelatedPerson resource is primarily used for attribution of information, since RelatedPersons are often a source of information about the patient. For keeping information about people for contact purposes for a patient, use a Patient's Contact element. Some individuals may serve as both a Patient's Contact and a Related Person.

Example RelatedPersons are:

* A patient's wife or husband
* A patient's relatives or friends
* A neighbor bringing a patient to the hospital
* The owner or trainer of a horse
* A patient's attorney or guardian
* A Guide Dog

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
        patient
      </td>

      <td style={{ textAlign: "left" }}>
        reference to patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        relationship
      </td>

      <td style={{ textAlign: "left" }}>
        [http://hl7.org/fhir/ValueSet/relatedperson-relationshiptype](http://hl7.org/fhir/ValueSet/relatedperson-relationshiptype)    

        The following codes are supported:\
        self|spouse|child|other|employee
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        * family  
        * given
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        telecom
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        gender
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        address
      </td>

      <td style={{ textAlign: "left" }}>
        will only display if the address is different than the patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        birthDate
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* RelatedPerson READ