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
Base Profile: <http://hl7.org/fhir/diagnosticreport.html>

The DiagnosticReport endpoint in FHIR is used to represent the findings and interpretation of diagnostic tests.  
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

This example provides a basic view of what a DiagnosticReport might look like, including references to related Patient and Observation resources.