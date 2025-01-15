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
Base profile: <https://www.hl7.org/fhir/task.html>

- Value Set: ValueSet/recall-action
- Value Set: ValueSet/task-type
- Value Set: ValueSet/recall-type

Currently the ‘Task’ resource can only be used to query and find Recalls in the ModMed Practice Management system. We will be expanding on the Task resource to include other types of tasks in the future, so if you are looking for additional functionality, be sure to check back.

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "unique identifier for the specific Task",
    "1-0": "lastUpdated",
    "1-1": "datetime the resource as last updated",
    "2-0": "status",
    "2-1": "ready|in-progress|completed   \n  \nThese are the fhir supported status fields they map in MMPM as follows:  \nready -> Open  \nin-progress -> Scheduled  \ncompleted -> closed  \n(overdue remains in ‘ready’ status)",
    "3-0": "statusReason",
    "3-1": "ValueSet:  \n{base_url}/{firm_url_prefix}ema/fhir/v2/ValueSet/recall-action",
    "4-0": "intent",
    "4-1": "‘unknown’ is the only supported value currently",
    "5-0": "code",
    "5-1": "ValueSet:  \n{base_url}/{firm_url_prefix}ema/fhir/v2/ValueSet/task-type  \nPMRECALL is the only supported type currently",
    "6-0": "description",
    "6-1": "string - free text field in MMPM for the ‘Reason’ for recall",
    "7-0": "for",
    "7-1": "reference to Patient",
    "8-0": "authoredOn",
    "8-1": "datetime",
    "9-0": "lastModified",
    "9-1": "datetime",
    "10-0": "requester",
    "10-1": "reference to Practitioner",
    "11-0": "reasonCode",
    "11-1": "ValueSet:  \n{base_url}/{firm_url_prefix}ema/fhir/v2/ValueSet/recall-type",
    "12-0": "note",
    "12-1": "string - free text field in MMPM for the Appt Notes in a recall",
    "13-0": "period",
    "13-1": "datetime - due date for the Recall"
  },
  "cols": 2,
  "rows": 14,
  "align": [
    "left",
    "left"
  ]
}
[/block]