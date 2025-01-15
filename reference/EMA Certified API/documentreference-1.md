---
title: DocumentReference
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
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-documentreference>

The FHIR (Fast Healthcare Interoperability Resources) DocumentReference resource is used in healthcare settings to reference and store documents such as reports, images, and other files relevant to patient care. This resource includes metadata about the document, such as the type of document, the patient it pertains to, and information on who created it.

### Key Components of the DocumentReference Resource

1. **Identifier**: Unique identifier for the document reference.
2. **Status**: The status of the document (e.g., current, superseded, entered-in-error).
3. **DocStatus**: Detailed doc status (e.g., preliminary, final, amended, entered-in-error).
4. **Type**: The type of document (e.g., discharge summary, image report).
5. **Category**: Additional categorization of the document (can be used for filtering or classification).
6. **Subject**: The patient or group the document is about.
7. **Date**: The date when this document was created.
8. **Author**: The person or organization who authored the document.
9. **Authenticator**: The individual who attested the document.
10. **Custodian**: Organization responsible for maintaining the document.
11. **Content**: Content details such as format, language, and URL to the document.
12. **Context**: Context or encounter associated with the document.

**Sample Response Object:**

```Text json
{  
  "resourceType": "DocumentReference",  
  "id": "example",  
  "status": "current",  
  "docStatus": "final",  
  "type": {  
    "coding": [  
      {  
        "system": "http://loinc.org",  
        "code": "34108-1",  
        "display": "Outpatient Note"  
      }  
    ],  
    "text": "Outpatient Note"  
  },  
  "category": \[  
    {  
      "coding": [  
        {  
          "system": "http://hl7.org/fhir/ValueSet/doc-typecodes",  
          "code": "clinical-note",  
          "display": "Clinical Note"  
        }  
      ]  
    }  
  ],  
  "subject": {  
    "reference": "Patient/12345",  
    "display": "John Doe"  
  },  
  "date": "2023-10-10T12:00:00Z",  
  "author": [  
    {  
      "reference": "Practitioner/abcd12",  
      "display": "Dr. Smith"  
    }  
  ],  
  "authenticator": {  
    "reference": "Practitioner/abcd12",  
    "display": "Dr. Smith"  
  },  
  "custodian": {  
    "reference": "Organization/1",  
    "display": "Health Clinic"  
  },  
  "content": [  
    {  
      "attachment": {  
        "contentType": "application/pdf",  
        "url": "http://example.org/fhir/document.pdf",  
        "title": "Clinical Note",  
        "creation": "2023-10-09T12:00:00Z"  
      }  
    }  
  ],  
  "context": {  
    "encounter": [  
      {  
        "reference": "Encounter/6789",  
        "display": "Consultation for John Doe"  
      }  
    ],  
    "event": {  
      "coding": [  
        {  
          "system": "http://snomed.info/sct",  
          "code": "308646001",  
          "display": "Encounter for symptom"  
        }  
      ]  
    }  
  }  
}
```

This JSON provides an overview of how to structure a DocumentReference resource including linking the document  
to a patient and providing detailed metadata.