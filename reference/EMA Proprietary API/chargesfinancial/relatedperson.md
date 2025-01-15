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
Base profile: <https://www.hl7.org/fhir/relatedperson.html>

RelatedPersons typically have a personal relationship or non-healthcare-specific professional relationship to the patient. A RelatedPerson resource is primarily used for attribution of information, since RelatedPersons are often a source of information about the patient. For keeping information about people for contact purposes for a patient, use a Patient's Contact element. Some individuals may serve as both a Patient's Contact and a Related Person.

Example RelatedPersons are:

- A patient's wife or husband
- A patient's relatives or friends
- A neighbor bringing a patient to the hospital
- The owner or trainer of a horse
- A patient's attorney or guardian
- A Guide Dog

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "",
    "1-0": "patient",
    "1-1": "reference to patient",
    "2-0": "relationship",
    "2-1": "<http://hl7.org/fhir/ValueSet/relatedperson-relationshiptype>    \n  \nThe following codes are supported:  \nself|spouse|child|other|employee",
    "3-0": "name",
    "3-1": "- family  \n- given",
    "4-0": "telecom",
    "4-1": "",
    "5-0": "gender",
    "5-1": "",
    "6-0": "address",
    "6-1": "will only display if the address is different than the patient",
    "7-0": "birthDate",
    "7-1": ""
  },
  "cols": 2,
  "rows": 8,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- RelatedPerson READ