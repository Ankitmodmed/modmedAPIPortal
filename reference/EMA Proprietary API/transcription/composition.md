---
title: Composition
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
Base profile: [https://www.hl7.org/fhir/composition.html](https://www.hl7.org/fhir/composition.html)

Currently, the **Composition** resource is used to facilitate inbound transcription. While its functionality is limited for now, additional capabilities will be introduced in future releases, so stay tuned for updates.

**Basic Functionality:**

* The Composition resource allows text to be added either to the Additional Visit Notes section of an in-progress visit or, if no visit is in progress, a Chart Note can be created for the patient.
* In both scenarios, the end user will be presented with a reconciliation interface to review and edit the text before it is incorporated into the note.

**Key Considerations:**

* To add text to an in-progress visit, you must provide the encounter reference.
* If there is no encounter or if the referenced encounter has a status of "finished," the Visit Note can no longer be edited.
* In such cases, when there is no encounter or the encounter is marked as "finished," the system will automatically create a new Chart Note for the patient.

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
        status
      </td>

      <td style={{ textAlign: "left" }}>
        preliminary - this is the only supported value at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        \{\
          "system": "[http://loinc.org](http://loinc.org)",\
          "code": "11488-4",\
          "display": "Consult note"\
        }\
        this is the only supported type at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        category
      </td>

      <td style={{ textAlign: "left" }}>
        \{\
          "system": "[http://loinc.org"](http://loinc.org"),\
          "code": "LP173421-1",\
          "display": "Report"\
        }\
        this is the only supported category at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        reference to Patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        encounter
      </td>

      <td style={{ textAlign: "left" }}>
        reference to Encounter
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
        author
      </td>

      <td style={{ textAlign: "left" }}>
        reference to the Practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        title
      </td>

      <td style={{ textAlign: "left" }}>
        This is a string which will become the Title of the Chart Note.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        section
      </td>

      <td style={{ textAlign: "left" }}>
        2 Sections are currently supported:  

        \{\
         "title": "Plan of treatment (narrative)",\
         "code": \{\
         "text": "Use this section as the body of your text",\
         "coding": \[\
         \{\
         "system": "[http://loinc.org"](http://loinc.org"),\
         "code": "18776-5",\
         "display": "Plan of treatment (narrative)",\
         }  

        \{\
         "title": "Instructions",\
         "code": \{\
         "text": "Use this section to communicate notes from the transcriptionist to the end user",\
         "coding": \[\
         \{\
         "system": "[http://loinc.org](http://loinc.org)",\
         "code": "69730-0",\
         "display": "Instructions"\
         }
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* Composition CREATE

The following attributes are required:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Name
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        status \*
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        preliminary is the only supported value at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type \*
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        \{\
          "system": "[http://loinc.org"](http://loinc.org"),\
          "code": "11488-4",\
          "display": "Consult note"\
        }\
        this is the only supported type at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        category \*
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        \{\
          "system": "[http://loinc.org"](http://loinc.org"),\
          "code": "LP173421-1",\
          "display": "Report"\
        }\
        this is the only supported category at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject \*
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>

      <td style={{ textAlign: "left" }}>
        Patient Reference
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        date\*
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        author \*
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>

      <td style={{ textAlign: "left" }}>
        Practitioner Reference
      </td>
    </tr>
  </tbody>
</Table>
