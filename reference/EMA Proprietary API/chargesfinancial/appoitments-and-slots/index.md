---
title: Appointments and Slots
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
## Appointments

Base profile: [http://hl7.org/fhir/StructureDefinition/Appointment](http://hl7.org/fhir/StructureDefinition/Appointment)

When scheduling an appointment, it’s essential to understand that an appointment can only be booked if there is a valid **Slot** available. Slots are configured based on the practice’s calendar settings. Different providers may have varying appointment durations for the same appointment type.

To successfully book an appointment, the following details are required:

* Appointment Type 
* Location 
* Provider 
* Patient 
* Date/Time 
* Duration

When querying available slots, providing just the **Appointment Type** is the minimum requirement. However, because each practice may configure its calendar differently, it’s recommended to include additional details like at least one **Practitioner**, one **Location**, and a date/time range for more accurate results.

***

### Appointment API Information

**Base URL:** \{base\_url}/\{firm\_url\_prefix}/ema/fhir/v2/Appointment

**Appointment Type ValueSet:**\
\{base\_url}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/appointment-type

* Appointment types are configured at the **firm level** and can be found by referencing the firm-specific appointment-type ValueSet.
* This ValueSet only returns **active** appointment types. If an expected type is missing, it may have been set to inactive.

**Reportable Reason ValueSet:**\
\{base\_url}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/reportable-reason

* Similarly, reportable reasons are configured at the firm level. Use the firm-specific reportable-reason ValueSet to find these reasons.

**Cancellation Reason ValueSet:**\
\{base\_url}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/appointment-cancellation-reason

***

### Common Use Cases

* Retrieve all appointments for a practice
* Find a specific appointment
* Create a new appointment
* Update the status of an appointment

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
        The MMI-specific unique identifier for the Appointment
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        FHIR supports the following statuses:\
        pending|booked|arrived|fulfilled|cancelled|noshow|entered-in-error|checked-in|waitlist  

        These statuses are mapped as follows in Modernizing Medicine’s Practice Management System UI:\
        pending = pending\
        booked = confirmed\
        arrived = arrived\
        fulfilled = checked-out\
        cancelled = cancelled\
        noshow = no show\
        entered-in-error = NOT SUPPORTED in MMPM\
        checked-in = checked in\
        waitlist = NOT SUPPORTED in MMPM
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        cancelationReason
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/appointment-cancellation-reason
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        appointment type
      </td>

      <td style={{ textAlign: "left" }}>
        Appointment Type ValueSet: \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/appointment-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reasonCode
      </td>

      <td style={{ textAlign: "left" }}>
        Reportable Reason Value Set: \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/reportable-reason
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        description
      </td>

      <td style={{ textAlign: "left" }}>
        Free text field that is mapped to the “Reason for Visit” field in MMPM. Max length for description is 100 characters
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        supportingInformation
      </td>

      <td style={{ textAlign: "left" }}>
        identifier: NEW\_PATIENT (true/false) boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        comment
      </td>

      <td style={{ textAlign: "left" }}>
        Free Text field that is mapped to the “Appointment Notes” field in MMPM\
        Max length for comment is 2048 characters
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        start
      </td>

      <td style={{ textAlign: "left" }}>
        Start Time and Date for the appointment
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        end
      </td>

      <td style={{ textAlign: "left" }}>
        End time and date for the appointment
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        minutesDuration
      </td>

      <td style={{ textAlign: "left" }}>
        Duration of the appointment in minutes
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        created
      </td>

      <td style={{ textAlign: "left" }}>
        Date and time the appointment was created
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        participant
      </td>

      <td style={{ textAlign: "left" }}>
        References to the Actors for the appointment:  

        * Location
        * Practitioner
        * Patient
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* Appointment READ
* Appointment SEARCH
* Appointment CREATE
* Appointment UPDATE

***

### Appointment CREATE

The minimum attributes for creating an appointment are:

<br />

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
        participant
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>

      <td style={{ textAlign: "left" }}>
        * Patient
        * Location
        * Practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        appointmentType
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet
      </td>

      <td style={{ textAlign: "left" }}>
        Appointment Type ValueSet: \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/appointment-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        start
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>

      <td style={{ textAlign: "left" }}>
        start time and date for the appointment
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        end
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>

      <td style={{ textAlign: "left" }}>
        end time and date for the appointment
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        minutesDuration
      </td>

      <td style={{ textAlign: "left" }}>
        integer
      </td>

      <td style={{ textAlign: "left" }}>
        Duration of the appointment in minutes
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        FHIR supports the following statuses:\
        pending|booked|arrived|fulfilled|cancelled|noshow|entered-in-error|checkedin|waitlist  

        These statuses are mapped as follows in Modernizing Medicine’s Practice Management System UI:\
        pending = pending\
        booked = confirmed\
        arrived = arrived\
        fulfilled = checked-out\
        cancelled = cancelled\
        noshow = no show\
        entered-in-error = NOT SUPPORTED in MMPM\
        checked-in = checked in\
        waitlist = NOT SUPPORTED in MMPM
      </td>
    </tr>
  </tbody>
</Table>

The payload of appointment create would generate this experience when someone at the practice went to view the created appointment:

![](https://files.readme.io/cecf7c6f857923e6f755093e951a986f155f24132304c34685b3512bcd81e844-image.png)

When creating Appointments users will also be able to push ‘Referring Provider’ as well as ‘Referral Source’ data within the context of the Appointment. This data would be sent within the ‘supportingInformation’ field.

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Name
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        supportingInformation
      </td>

      <td style={{ textAlign: "left" }}>
        identifier: NEW\_PATIENT (true/false) boolean  

        Reference to Practitioner(referring Provider) or Reference to Organization(Referring Institution).\
        This is optional data.  

        Referral-Source identifier which is a ValueSet\
        \{firm\_url\_prefix}/ema/fhir/v2/ValueSet/referral-source
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

***

### Appointment UPDATE

Fields accepted for updating an appointment are:

<br />

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
        description
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        updates the “reason for visit” field in MMPM
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        minutesDuration
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        updates the duration of an appointment
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        start
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        end
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        FHIR supports the following statuses:\
        pending|booked|arrived|fulfilled|cancelled|noshow|entered-in-error|checkedin|waitlist  

        These statuses are mapped as follows in Modernizing Medicine’s Practice Management System UI:\
        pending = pending\
        booked = confirmed\
        arrived = arrived\
        fulfilled = checked-out\
        cancelled = cancelled\
        noshow = no show\
        entered-in-error = NOT SUPPORTED in MMPM\
        checked-in = checked in\
        waitlist = NOT SUPPORTED in MMPM
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reportableReason
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        description
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        supportingInformation
      </td>

      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        identifier: NEW\_PATIENT (true/false) boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        comment
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        cancelationReason
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/appointment-cancellation-reason
      </td>
    </tr>
  </tbody>
</Table>
