---
title: Tasks/Recalls
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
Base profile: [https://www.hl7.org/fhir/task.html](https://www.hl7.org/fhir/task.html)

* Value Set: ValueSet/recall-action
* Value Set: ValueSet/task-type
* Value Set: ValueSet/recall-type

Currently the ‘Task’ resource can only be used to query and find Recalls in the ModMed Practice Management system. We will be expanding on the Task resource to include other types of tasks in the future, so if you are looking for additional functionality, be sure to check back.

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
        unique identifier for the specific Task
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        lastUpdated
      </td>

      <td style={{ textAlign: "left" }}>
        datetime the resource as last updated
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        ready|in-progress|completed   

        These are the fhir supported status fields they map in MMPM as follows:\
        ready -> Open\
        in-progress -> Scheduled\
        completed -> closed\
        (overdue remains in ‘ready’ status)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        statusReason
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet:\
        \{base\_url}/\{firm\_url\_prefix}ema/fhir/v2/ValueSet/recall-action
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        intent
      </td>

      <td style={{ textAlign: "left" }}>
        ‘unknown’ is the only supported value currently
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet:\
        \{base\_url}/\{firm\_url\_prefix}ema/fhir/v2/ValueSet/task-type\
        PMRECALL is the only supported type currently
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        description
      </td>

      <td style={{ textAlign: "left" }}>
        string - free text field in MMPM for the ‘Reason’ for recall
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        for
      </td>

      <td style={{ textAlign: "left" }}>
        reference to Patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        authoredOn
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        lastModified
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        requester
      </td>

      <td style={{ textAlign: "left" }}>
        reference to Practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reasonCode
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet:\
        \{base\_url}/\{firm\_url\_prefix}ema/fhir/v2/ValueSet/recall-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        note
      </td>

      <td style={{ textAlign: "left" }}>
        string - free text field in MMPM for the Appt Notes in a recall
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        period
      </td>

      <td style={{ textAlign: "left" }}>
        datetime - due date for the Recall
      </td>
    </tr>
  </tbody>
</Table>
