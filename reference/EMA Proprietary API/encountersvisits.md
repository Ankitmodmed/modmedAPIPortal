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
Base profile: <https://www.hl7.org/fhir/encounter.html>

### Understanding Visits and Encounters

Visits, including **Telehealth visits** and **Non-Visit Orders**, are represented in the /Encounter resource. It's important to note that **Encounters** are distinct from **Appointments**. Think of an appointment as a placeholder for a potential encounter.

- **Standard Workflow:**  
  When an encounter is created from an appointment (which is the typical workflow), there will be a reference link between the two. However, in cases where a user deviates from the standard process, this link may not exist.
- **Non-PM System Practices:**  
  If the practice is not using our Practice Management (PM) system, MMPM, then the appointment data will not be linked to the encounter resource.
- **Encounter Status:**  
  While an encounter is still in progress, you will not be able to retrieve the **Visit Note **(document) or the **Charges** (`ChargeItems`). These details only become available once the encounter is marked as "finished."

Common use cases include:

- Find all Encounters (visits) for a patient

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "unique encounter ID",
    "1-0": "metadata  \n  \n- lastUpdated",
    "1-1": "time/date the encounter was last updated",
    "2-0": "status",
    "2-1": "FHIR supports the following statuses: planned | arrived | triaged | in-progress | onleave | finished | cancelled +  \nCurrently MMI will only support encounters which are : ‘finished’ or ‘in-progress’",
    "3-0": "class",
    "3-1": "<https://www.hl7.org/fhir/v3/ActEncounterCode/vs.html>  \nCurrently MMI will only support the class of ‘AMB’",
    "4-0": "type",
    "4-1": "Encounter Type ValueSet:  \n{baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/encounter-type",
    "5-0": "subject",
    "5-1": "Reference: Patient",
    "6-0": "participant  \n  \n- individual",
    "6-1": "Reference: Practitioner",
    "7-0": "appointment",
    "7-1": "Reference: Appointment  \nNote: that this will only appear if the appointment was created using MMPM AND the Encounter/Visit was created through the Appointment.",
    "8-0": "period",
    "8-1": "start: datetime the Encounter was started  \nend: datetime the Encounter was finalized",
    "9-0": "diagnosis  \n  \n- condition",
    "9-1": "Reference: Condition  \nNote: When the Encounter is still ‘in-progress’, the Diagnoses will be identified by the ICD10 codes and once the Encounter is ‘finished’, those diagnoses will become References to the Condition resource.",
    "10-0": "location",
    "10-1": "Reference: Location"
  },
  "cols": 2,
  "rows": 11,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- Encounter READ
- Encounter SEARCH