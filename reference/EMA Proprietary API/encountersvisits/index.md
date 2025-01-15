---
title: Encounters/Visits
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
Base profile: [https://www.hl7.org/fhir/encounter.html](https://www.hl7.org/fhir/encounter.html)

### Understanding Visits and Encounters

Visits, including **Telehealth visits** and **Non-Visit Orders**, are represented in the /Encounter resource. It's important to note that **Encounters** are distinct from **Appointments**. Think of an appointment as a placeholder for a potential encounter.

* **Standard Workflow:**\
  When an encounter is created from an appointment (which is the typical workflow), there will be a reference link between the two. However, in cases where a user deviates from the standard process, this link may not exist.
* **Non-PM System Practices:**\
  If the practice is not using our Practice Management (PM) system, MMPM, then the appointment data will not be linked to the encounter resource.
* **Encounter Status:**\
  While an encounter is still in progress, you will not be able to retrieve the **Visit Note** (document) or the **Charges** (`ChargeItems`). These details only become available once the encounter is marked as "finished."

Common use cases include:

* Find all Encounters (visits) for a patient

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
        unique encounter ID
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        metadata  

        * lastUpdated
      </td>

      <td style={{ textAlign: "left" }}>
        time/date the encounter was last updated
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        FHIR supports the following statuses: planned | arrived | triaged | in-progress | onleave | finished | cancelled +\
        Currently MMI will only support encounters which are : ‘finished’ or ‘in-progress’
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        class
      </td>

      <td style={{ textAlign: "left" }}>
        [https://www.hl7.org/fhir/v3/ActEncounterCode/vs.html](https://www.hl7.org/fhir/v3/ActEncounterCode/vs.html)\
        Currently MMI will only support the class of ‘AMB’
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        Encounter Type ValueSet:\
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/encounter-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        Reference: Patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        participant  

        * individual
      </td>

      <td style={{ textAlign: "left" }}>
        Reference: Practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        appointment
      </td>

      <td style={{ textAlign: "left" }}>
        Reference: Appointment\
        Note: that this will only appear if the appointment was created using MMPM AND the Encounter/Visit was created through the Appointment.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        period
      </td>

      <td style={{ textAlign: "left" }}>
        start: datetime the Encounter was started\
        end: datetime the Encounter was finalized
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        diagnosis  

        * condition
      </td>

      <td style={{ textAlign: "left" }}>
        Reference: Condition\
        Note: When the Encounter is still ‘in-progress’, the Diagnoses will be identified by the ICD10 codes and once the Encounter is ‘finished’, those diagnoses will become References to the Condition resource.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        location
      </td>

      <td style={{ textAlign: "left" }}>
        Reference: Location
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* Encounter READ
* Encounter SEARCH
