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

Base profile: <http://hl7.org/fhir/StructureDefinition/Appointment>

When scheduling an appointment, it’s essential to understand that an appointment can only be booked if there is a valid **Slot** available. Slots are configured based on the practice’s calendar settings. Different providers may have varying appointment durations for the same appointment type.

To successfully book an appointment, the following details are required:

- Appointment Type 
- Location 
- Provider 
- Patient 
- Date/Time 
- Duration

When querying available slots, providing just the **Appointment Type** is the minimum requirement. However, because each practice may configure its calendar differently, it’s recommended to include additional details like at least one **Practitioner**, one **Location**, and a date/time range for more accurate results.

***

### Appointment API Information

**Base URL:** {base_url}/{firm_url_prefix}/ema/fhir/v2/Appointment

**Appointment Type ValueSet:**  
{base_url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/appointment-type

- Appointment types are configured at the **firm level **and can be found by referencing the firm-specific appointment-type ValueSet.
- This ValueSet only returns **active** appointment types. If an expected type is missing, it may have been set to inactive.

**Reportable Reason ValueSet:**  
{base_url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/reportable-reason

- Similarly, reportable reasons are configured at the firm level. Use the firm-specific reportable-reason ValueSet to find these reasons.

**Cancellation Reason ValueSet:**  
{base_url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/appointment-cancellation-reason

***

### Common Use Cases

- Retrieve all appointments for a practice
- Find a specific appointment
- Create a new appointment
- Update the status of an appointment

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The MMI-specific unique identifier for the Appointment",
    "1-0": "status",
    "1-1": "FHIR supports the following statuses:  \npending|booked|arrived|fulfilled|cancelled|noshow|entered-in-error|checked-in|waitlist  \n  \nThese statuses are mapped as follows in Modernizing Medicine’s Practice Management System UI:  \npending = pending  \nbooked = confirmed  \narrived = arrived  \nfulfilled = checked-out  \ncancelled = cancelled  \nnoshow = no show  \nentered-in-error = NOT SUPPORTED in MMPM  \nchecked-in = checked in  \nwaitlist = NOT SUPPORTED in MMPM",
    "2-0": "cancelationReason",
    "2-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/appointment-cancellation-reason",
    "3-0": "appointment type",
    "3-1": "Appointment Type ValueSet: {baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/appointment-type",
    "4-0": "reasonCode",
    "4-1": "Reportable Reason Value Set: {baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/reportable-reason",
    "5-0": "description",
    "5-1": "Free text field that is mapped to the “Reason for Visit” field in MMPM. Max length for description is 100 characters",
    "6-0": "supportingInformation",
    "6-1": "identifier: NEW_PATIENT (true/false) boolean",
    "7-0": "comment",
    "7-1": "Free Text field that is mapped to the “Appointment Notes” field in MMPM  \nMax length for comment is 2048 characters",
    "8-0": "start",
    "8-1": "Start Time and Date for the appointment",
    "9-0": "end",
    "9-1": "End time and date for the appointment",
    "10-0": "minutesDuration",
    "10-1": "Duration of the appointment in minutes",
    "11-0": "created",
    "11-1": "Date and time the appointment was created",
    "12-0": "participant",
    "12-1": "References to the Actors for the appointment:  \n  \n- Location\n- Practitioner\n- Patient"
  },
  "cols": 2,
  "rows": 13,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- Appointment READ
- Appointment SEARCH
- Appointment CREATE
- Appointment UPDATE

***

### Appointment CREATE

The minimum attributes for creating an appointment are:

<br />

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "participant",
    "0-1": "reference",
    "0-2": "- Patient\n- Location\n- Practitioner",
    "1-0": "appointmentType",
    "1-1": "ValueSet",
    "1-2": "Appointment Type ValueSet: {baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/appointment-type",
    "2-0": "start",
    "2-1": "datetime",
    "2-2": "start time and date for the appointment",
    "3-0": "end",
    "3-1": "datetime",
    "3-2": "end time and date for the appointment",
    "4-0": "minutesDuration",
    "4-1": "integer",
    "4-2": "Duration of the appointment in minutes",
    "5-0": "status",
    "5-1": "code",
    "5-2": "FHIR supports the following statuses:  \npending|booked|arrived|fulfilled|cancelled|noshow|entered-in-error|checkedin|waitlist  \n  \nThese statuses are mapped as follows in Modernizing Medicine’s Practice Management System UI:  \npending = pending  \nbooked = confirmed  \narrived = arrived  \nfulfilled = checked-out  \ncancelled = cancelled  \nnoshow = no show  \nentered-in-error = NOT SUPPORTED in MMPM  \nchecked-in = checked in  \nwaitlist = NOT SUPPORTED in MMPM"
  },
  "cols": 3,
  "rows": 6,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


The payload of appointment create would generate this experience when someone at the practice went to view the created appointment:

![](https://files.readme.io/cecf7c6f857923e6f755093e951a986f155f24132304c34685b3512bcd81e844-image.png)

When creating Appointments users will also be able to push ‘Referring Provider’ as well as ‘Referral Source’ data within the context of the Appointment. This data would be sent within the ‘supportingInformation’ field.

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Description",
    "0-0": "supportingInformation",
    "0-1": "identifier: NEW_PATIENT (true/false) boolean  \n  \nReference to Practitioner(referring Provider) or Reference to Organization(Referring Institution).  \nThis is optional data.  \n  \nReferral-Source identifier which is a ValueSet  \n{firm_url_prefix}/ema/fhir/v2/ValueSet/referral-source",
    "1-0": "",
    "1-1": ""
  },
  "cols": 2,
  "rows": 2,
  "align": [
    "left",
    "left"
  ]
}
[/block]


***

### Appointment UPDATE

Fields accepted for updating an appointment are:

<br />

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "description",
    "0-1": "string",
    "0-2": "updates the “reason for visit” field in MMPM",
    "1-0": "minutesDuration",
    "1-1": "string",
    "1-2": "updates the duration of an appointment",
    "2-0": "start",
    "2-1": "datetime",
    "2-2": "",
    "3-0": "end",
    "3-1": "datetime",
    "3-2": "",
    "4-0": "status",
    "4-1": "code",
    "4-2": "FHIR supports the following statuses:  \npending|booked|arrived|fulfilled|cancelled|noshow|entered-in-error|checkedin|waitlist  \n  \nThese statuses are mapped as follows in Modernizing Medicine’s Practice Management System UI:  \npending = pending  \nbooked = confirmed  \narrived = arrived  \nfulfilled = checked-out  \ncancelled = cancelled  \nnoshow = no show  \nentered-in-error = NOT SUPPORTED in MMPM  \nchecked-in = checked in  \nwaitlist = NOT SUPPORTED in MMPM",
    "5-0": "reportableReason",
    "5-1": "string",
    "5-2": "",
    "6-0": "description",
    "6-1": "string",
    "6-2": "",
    "7-0": "supportingInformation",
    "7-1": "identifier",
    "7-2": "identifier: NEW_PATIENT (true/false) boolean",
    "8-0": "comment",
    "8-1": "string",
    "8-2": "",
    "9-0": "cancelationReason",
    "9-1": "code",
    "9-2": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/appointment-cancellation-reason"
  },
  "cols": 3,
  "rows": 10,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]