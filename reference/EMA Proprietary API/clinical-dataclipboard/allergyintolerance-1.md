---
title: AllergyIntolerance
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
Base profile: <https://www.hl7.org/fhir/allergyintolerance.html>

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "clinicalStatus",
    "0-1": "active | inactive | resolved",
    "1-0": "code",
    "1-1": "MMI uses several sources to populate Allergies in EMA. RxNorm is used for medication allergies.  \nYou may see additional codes returned for other allergy types.",
    "2-0": "patient",
    "2-1": "Reference to Patient",
    "3-0": "onset  \n  \n- onsetDateTime\n- lastOccurrence",
    "3-1": "",
    "4-0": "recordedDate",
    "4-1": "Date Recorded",
    "5-0": "reaction",
    "5-1": "",
    "6-0": "reaction.manifestation",
    "6-1": "Anaphylaxis (417516000) |Angioedema(41291007)|Diarrhea(62315008)|Dizziness( 404640003)|Fatigue(84229001)|GI upset(162059005)| Hives(126485001)|Liver toxicity (197354009)|Nausea(422587007)|Rash (162415008)|Shortness of breath(267036007)|Swelling(65124004)|Weal(247472004)|Other(419199007) - SNOMED CT (these are mapped in EMA)",
    "7-0": "reaction.severity",
    "7-1": "unspecified|mild|mild to moderate|moderate|moderate to severe|severe|fatal - Use SNOMED CT  \nPLEASE NOTE: Since FHIR only supports mild|moderate|severe, EMA fields are mapped as followed:    \n  \n- unspecified : will return no value  \n- mild=mild  \n- mild to moderate = mild  \n- moderate =moderate  \n- moderate to severe = moderate  \n- severe = severe  \n- fatal = severe",
    "8-0": "reaction.substance",
    "8-1": "code",
    "9-0": "reaction.description",
    "9-1": "narrative text box"
  },
  "cols": 2,
  "rows": 10,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- AllergyIntolerance READ
- AllergyIntolerance SEARCH
- AllergyIntolerance CREATE
- AllergyIntolerance UPDATE

***

### AllergyIntolerance CREATE

Note that Allergies added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

***

### AllergyIntolerance UPDATE

Note that Allergies added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.