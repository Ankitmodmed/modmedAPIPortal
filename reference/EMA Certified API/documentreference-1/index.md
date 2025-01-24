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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-documentreference](http://hl7.org/fhir/us/core/StructureDefinition/us-core-documentreference)

A DocumentReference resource is used to index a document, clinical note, and other binary objects to make them available to a healthcare system.It can be used with any document format that has a recognized mime type and that conforms to this definition.

Read more from : [https://hl7.org/fhir/R4/documentreference.html](https://hl7.org/fhir/R4/documentreference.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "DocumentReference",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "masterIdentifier" : { Identifier }, // Master Version Specific Identifier
  "identifier" : [{ Identifier }], // Other identifiers for the document
  "status" : "<code>", // R!  current | superseded | entered-in-error
  "docStatus" : "<code>", // preliminary | final | amended | entered-in-error
  "type" : { CodeableConcept }, // Kind of document (LOINC if possible)
  "category" : [{ CodeableConcept }], // Categorization of document
  "subject" : { Reference(Patient|Practitioner|Group|Device) }, // Who/what is the subject of the document
  "date" : "<instant>", // When this document reference was created
  "author" : [{ Reference(Practitioner|PractitionerRole|Organization|Device|
   Patient|RelatedPerson) }], // Who and/or what authored the document
  "authenticator" : { Reference(Practitioner|PractitionerRole|Organization) }, // Who/what authenticated the document
  "custodian" : { Reference(Organization) }, // Organization which maintains the document
  "relatesTo" : [{ // Relationships to other documents
    "code" : "<code>", // R!  replaces | transforms | signs | appends
    "target" : { Reference(DocumentReference) } // R!  Target of the relationship
  }],
  "description" : "<string>", // Human-readable description
  "securityLabel" : [{ CodeableConcept }], // Document security-tags
  "content" : [{ // R!  Document referenced
    "attachment" : { Attachment }, // R!  Where to access the document
    "format" : { Coding } // Format/content rules for the document
  }],
  "context" : { // Clinical context of document
    "encounter" : [{ Reference(Encounter|EpisodeOfCare) }], // Context of the document  content
    "event" : [{ CodeableConcept }], // Main clinical acts documented
    "period" : { Period }, // Time of service that is being documented
    "facilityType" : { CodeableConcept }, // Kind of facility where patient was seen
    "practiceSetting" : { CodeableConcept }, // Additional details about where the content was created (e.g. clinical specialty)
    "sourcePatientInfo" : { Reference(Patient) }, // Patient demographics from source
    "related" : [{ Reference(Any) }] // Related identifiers or resources
  }
}
```

This JSON provides an overview of how to structure a DocumentReference resource including linking the document\
to a patient and providing detailed metadata.