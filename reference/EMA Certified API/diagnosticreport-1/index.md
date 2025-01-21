---
title: DiagnosticReport
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
Base Profile: [http://hl7.org/fhir/diagnosticreport.html](http://hl7.org/fhir/diagnosticreport.html)

The DiagnosticReport endpoint in FHIR is used to represent the findings and interpretation of diagnostic tests.\
Key components of a DiagnosticReport resource include:

1. **Resource identification and metadata**:

```
- id: Logical id of the resource.
- meta: Metadata about the resource, such as version and last updated time.
```

2. **Status**: The status of the diagnostic report (e.g., registered, partial, preliminary, final, amended, corrected).
3. **Category**: The general nature of the diagnostic report (e.g., Radiology, Pathology).
4. **Code**: The specific type of report (e.g., a chest x-ray report).
5. **Subject**: Who or what the report is about (usually a patient).
6. **Effective**: The time or time period when the diagnostic observations were made.
7. **Issued**: The date and time this version of the report was released.
8. **Performer**: Who was responsible for the report.
9. **Results**: Link to results as Observation resources.

<br />

New content:

A diagnostic report is the set of information that is typically provided by a diagnostic service when investigations are complete. The information includes a mix of atomic results, text reports, images, and codes. The mix varies depending on the nature of the diagnostic procedure, and sometimes on the nature of the outcomes for a particular investigation.

Read more from : [https://hl7.org/fhir/diagnosticreport.html](https://hl7.org/fhir/diagnosticreport.html)

<br />

**Sample Response Object:**

```Text json
{  
  "resourceType": "DiagnosticReport",  
  "id": "example",  
  "meta": {  
    "versionId": "1",  
    "lastUpdated": "2023-10-03T10:00:00Z"  
  },  
  "status": "final",  
  "category": {  
    "coding": [  
      {  
        "system": "http://terminology.hl7.org/CodeSystem/v2-0074",  
        "code": "RAD",  
        "display": "Radiology"  
      }  
    ]  
  },  
  "code": {  
    "coding": [  
      {  
        "system": "http://loinc.org",  
        "code": "45090-7",  
        "display": "Chest X-ray Report"  
      }  
    ]  
  },  
  "subject": {  
    "reference": "Patient/1234",  
    "display": "John Doe"  
  },  
  "effectiveDateTime": "2023-10-01T09:00:00Z",  
  "issued": "2023-10-03T09:45:00Z",  
  "performer": [  
    {  
      "reference": "Practitioner/456",  
      "display": "Dr. Jane Smith"  
    }  
  ],  
  "result": [  
    {  
      "reference": "Observation/987",  
      "display": "Chest X-ray findings"  
    }  
  ]  
}  
```
```json new json
{
  "resourceType" : "DiagnosticReport",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business identifier for report
  "basedOn" : [{ Reference(CarePlan|ImmunizationRecommendation|
   MedicationRequest|NutritionOrder|ServiceRequest) }], // What was requested
  "status" : "<code>", // R!  registered | partial | preliminary | modified | final | amended | corrected | appended | cancelled | entered-in-error | unknown
  "category" : [{ CodeableConcept }], // Service category
  "code" : { CodeableConcept }, // R!  Name/Code for this diagnostic report
  "subject" : { Reference(BiologicallyDerivedProduct|Device|Group|Location|
   Medication|Organization|Patient|Practitioner|Substance) }, // The subject of the report - usually, but not always, the patient
  "encounter" : { Reference(Encounter) }, // Health care event when test ordered
  // effective[x]: Clinically relevant time/time-period for report. One of these 2:
  "effectiveDateTime" : "<dateTime>",
  "effectivePeriod" : { Period },
  "issued" : "<instant>", // DateTime this version was made
  "performer" : [{ Reference(CareTeam|Organization|Practitioner|
   PractitionerRole) }], // Responsible Diagnostic Service
  "resultsInterpreter" : [{ Reference(CareTeam|Organization|Practitioner|
   PractitionerRole) }], // Primary result interpreter
  "specimen" : [{ Reference(Specimen) }], // Specimens this report is based on
  "result" : [{ Reference(Observation) }], // I Observations
  "note" : [{ Annotation }], // Comments about the diagnostic report
  "study" : [{ Reference(GenomicStudy|ImagingStudy) }], // Reference to full details of an analysis associated with the diagnostic report
  "supportingInfo" : [{ // Additional information supporting the diagnostic report
    "type" : { CodeableConcept }, // R!  Supporting information role code icon
    "reference" : { Reference(Citation|DiagnosticReport|Observation|Procedure) } // R!  Supporting information reference
  }],
  "media" : [{ // Key images or data associated with this report
    "comment" : "<string>", // Comment about the image or data (e.g. explanation)
    "link" : { Reference(DocumentReference) } // R!  Reference to the image or data source
  }],
  "composition" : { Reference(Composition) }, // I Reference to a Composition resource for the DiagnosticReport structure
  "conclusion" : "<markdown>", // Clinical conclusion (interpretation) of test results
  "conclusionCode" : [{ CodeableConcept }], // Codes for the clinical conclusion of test results
  "presentedForm" : [{ Attachment }] // Entire report as issued
}
```

This example provides a basic view of what a DiagnosticReport might look like, including references to related Patient and Observation resources.