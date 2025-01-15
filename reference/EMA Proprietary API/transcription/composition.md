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
Base profile: <https://www.hl7.org/fhir/composition.html>

Currently, the **Composition** resource is used to facilitate inbound transcription. While its functionality is limited for now, additional capabilities will be introduced in future releases, so stay tuned for updates.

**Basic Functionality:**

- The Composition resource allows text to be added either to the Additional Visit Notes section of an in-progress visit or, if no visit is in progress, a Chart Note can be created for the patient.
- In both scenarios, the end user will be presented with a reconciliation interface to review and edit the text before it is incorporated into the note.

**Key Considerations:**

- To add text to an in-progress visit, you must provide the encounter reference.
- If there is no encounter or if the referenced encounter has a status of "finished," the Visit Note can no longer be edited.
- In such cases, when there is no encounter or the encounter is marked as "finished," the system will automatically create a new Chart Note for the patient.

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "status",
    "0-1": "preliminary - this is the only supported value at this time",
    "1-0": "type",
    "1-1": "{  \n  \"system\": \"<http://loinc.org>\",  \n  \"code\": \"11488-4\",  \n  \"display\": \"Consult note\"  \n}  \nthis is the only supported type at this time",
    "2-0": "category",
    "2-1": "{  \n  \"system\": \"<http://loinc.org\">,  \n  \"code\": \"LP173421-1\",  \n  \"display\": \"Report\"  \n}  \nthis is the only supported category at this time",
    "3-0": "subject",
    "3-1": "reference to Patient",
    "4-0": "encounter",
    "4-1": "reference to Encounter",
    "5-0": "date",
    "5-1": "datetime",
    "6-0": "author",
    "6-1": "reference to the Practitioner",
    "7-0": "title",
    "7-1": "This is a string which will become the Title of the Chart Note.",
    "8-0": "section",
    "8-1": "2 Sections are currently supported:  \n  \n{  \n \"title\": \"Plan of treatment (narrative)\",  \n \"code\": {  \n \"text\": \"Use this section as the body of your text\",  \n \"coding\": \\[  \n {  \n \"system\": \"<http://loinc.org\">,  \n \"code\": \"18776-5\",  \n \"display\": \"Plan of treatment (narrative)\",  \n }  \n  \n{  \n \"title\": \"Instructions\",  \n \"code\": {  \n \"text\": \"Use this section to communicate notes from the transcriptionist to the end user\",  \n \"coding\": \\[  \n {  \n \"system\": \"<http://loinc.org>\",  \n \"code\": \"69730-0\",  \n \"display\": \"Instructions\"  \n }"
  },
  "cols": 2,
  "rows": 9,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- Composition CREATE

The following attributes are required:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "status \\*",
    "0-1": "code",
    "0-2": "preliminary is the only supported value at this time",
    "1-0": "type \\*",
    "1-1": "code",
    "1-2": "{  \n  \"system\": \"<http://loinc.org\">,  \n  \"code\": \"11488-4\",  \n  \"display\": \"Consult note\"  \n}  \nthis is the only supported type at this time",
    "2-0": "category \\*",
    "2-1": "code",
    "2-2": "{  \n  \"system\": \"<http://loinc.org\">,  \n  \"code\": \"LP173421-1\",  \n  \"display\": \"Report\"  \n}  \nthis is the only supported category at this time",
    "3-0": "subject \\*",
    "3-1": "reference",
    "3-2": "Patient Reference",
    "4-0": "date\\*",
    "4-1": "datetime",
    "4-2": "datetime",
    "5-0": "author \\*",
    "5-1": "reference",
    "5-2": "Practitioner Reference"
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