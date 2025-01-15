---
title: Procedure
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
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-procedure>

The Procedure resource in FHIR represents an action that is being, has been, or is scheduled to be performed on a patient. Examples of procedures include surgeries, therapies, diagnostic actions, and more.

## Key Components of FHIR Procedure Resource

1. **Identifier**: Unique identifier for the procedure.
2. **Status**: Indicates the current state of the procedure (e.g., preparation, in progress, completed, entered-in-error, etc.).
3. **Category**: Broad categorization of the type of procedure (e.g., surgical, laboratory, etc.).
4. **Code**: A specific code or description identifying the procedure.
5. **Subject**: The patient, implying whom the procedure is performed on.
6. **Encounter**: The encounter during which the procedure was performed.
7. **Performed**: The period of time during which the procedure was performed.
8. **Performer**: Individual(s) who performed the procedure.
9. **ReasonCode**: The reason why the procedure was performed.
10. **BodySite**: Target body site where the procedure was performed.
11. **Outcome**: The result or outcome of the procedure.
12. **Report**: Any report generated as a result of the procedure.
13. **Complication**: Any complications experienced during the procedure.
14. **FollowUp**: Instructions or information regarding follow-up care.

**Sample Response Object:**

```Text json
{
 "resourceType": "Procedure",
 "id": "example",
 "status": "completed",
 "category": {
   "coding": [
     {
       "system": "http://snomed.info/sct",
       "code": "103693007",
       "display": "Diagnostic procedure"
     }
   ],
   "text": "Diagnostic procedure"
 },
 "code": {
   "coding": [
     {
       "system": "http://snomed.info/sct",
       "code": "80146002",
       "display": "Appendectomy"
     }
   ],
   "text": "Appendectomy"
 },
 "subject": {
   "reference": "Patient/example"
 },
 "encounter": {
   "reference": "Encounter/example"
 },
 "performedPeriod": {
   "start": "2014-08-16T06:00:00Z",
   "end": "2014-08-16T07:30:00Z"
 },
 "performer": [
   {
     "actor": {
       "reference": "Practitioner/example",
       "display": "Dr. John Doe"
     },
     "role": {
       "coding": [
         {
           "system": "http://terminology.hl7.org/CodeSystem/v2-0412",
           "code": "01",
           "display": "Primary surgeon"
         }
       ]
     }
   }
 ],
 "reasonCode": [
   {
     "coding": [
       {
         "system": "http://snomed.info/sct",
         "code": "233604007",
         "display": "Acute appendicitis"
       }
     ],
     "text": "Acute appendicitis"
   }
 ],
 "outcome": {
   "coding": [
     {
       "system": "http://snomed.info/sct",
       "code": "301608005",
       "display": "Appendix removed"
     }
   ],
"text": "Appendix removed"
 }
}
```