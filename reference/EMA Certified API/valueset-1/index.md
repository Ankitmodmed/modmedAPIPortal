---
title: ValueSet
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
Base Profile: [https://www.hl7.org/fhir/valueset.html](https://www.hl7.org/fhir/valueset.html)

The FHIR Procedure resource is used to record detailed information about actions performed on patients.

## Key Components of the FHIR Procedure Resource

1. **Resource ID**: Unique identifier for the procedure.
2. **Status**: The current state of the procedure (e.g., completed, in-progress).
3. **Code**: The specific code representing the procedure (often using a standardized coding system).
4. **Subject**: The patient subject to the procedure.
5. **Performer**: Who performed the procedure.
6. **Performed**: Date/Period when the procedure was performed.
7. **Reason**: Reason for performing the procedure.
8. **Body Site**: The body site on which the procedure was performed.
9. **Outcome**: The result or outcome of the procedure.

New content:

A ValueSet resource instance specifies a set of codes drawn from one or more code systems, intended for use in a particular context.

Read more from: [https://www.hl7.org/fhir/valueset.html](https://www.hl7.org/fhir/valueset.html)

<br />

**Sample Response Object:**

```Text json
{
  "resourceType": "Procedure",
  "id": "example",
  "status": "completed",
  "code": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "80146002",
        "display": "Appendectomy (procedure)"
      }
    ],
    "text": "Appendectomy"
  },
  "subject": {
    "reference": "Patient/example"
  },
  "performedPeriod": {
    "start": "2022-02-01T10:30:00+01:00",
    "end": "2022-02-01T11:30:00+01:00"
  },
  "performer": [
    {
      "actor": {
        "reference": "Practitioner/example"
      }
    }
  ],
  "reasonCode": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "233604007",
          "display": "Appendicitis"
        }
      ],
      "text": "Appendicitis"
    }
  ],
  "bodySite": [
    {
      "coding": [
        {
          "system": "http://snomed.info/sct",
          "code": "78961009",
          "display": "Abdomen"
        }
      ],
      "text": "Abdomen"
    }
  ],
  "outcome": {
    "text": "Procedure was successful"
  }
}
```
```json new json
{
  "resourceType" : "ValueSet",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "url" : "<uri>", // Canonical identifier for this value set, represented as a URI (globally unique)
  "identifier" : [{ Identifier }], // Additional identifier for the value set (business identifier)
  "version" : "<string>", // Business version of the value set
  // versionAlgorithm[x]: How to compare versions. One of these 2:
  "versionAlgorithmString" : "<string>",
  "versionAlgorithmCoding" : { Coding },
  "name" : "<string>", // I Name for this value set (computer friendly)
  "title" : "<string>", // Name for this value set (human friendly)
  "status" : "<code>", // R!  draft | active | retired | unknown
  "experimental" : <boolean>, // For testing purposes, not real usage
  "date" : "<dateTime>", // Date last changed
  "publisher" : "<string>", // Name of the publisher/steward (organization or individual)
  "contact" : [{ ContactDetail }], // Contact details for the publisher
  "description" : "<markdown>", // Natural language description of the value set
  "useContext" : [{ UsageContext }], // The context that the content is intended to support
  "jurisdiction" : [{ CodeableConcept }], // Intended jurisdiction for value set (if applicable)
  "immutable" : <boolean>, // Indicates whether or not any change to the content logical definition may occur
  "purpose" : "<markdown>", // Why this value set is defined
  "copyright" : "<markdown>", // Use and/or publishing restrictions
  "copyrightLabel" : "<string>", // Copyright holder and year(s)
  "approvalDate" : "<date>", // When the ValueSet was approved by publisher
  "lastReviewDate" : "<date>", // When the ValueSet was last reviewed by the publisher
  "effectivePeriod" : { Period }, // When the ValueSet is expected to be used
  "topic" : [{ CodeableConcept }], // E.g. Education, Treatment, Assessment, etc
  "author" : [{ ContactDetail }], // Who authored the ValueSet
  "editor" : [{ ContactDetail }], // Who edited the ValueSet
  "reviewer" : [{ ContactDetail }], // Who reviewed the ValueSet
  "endorser" : [{ ContactDetail }], // Who endorsed the ValueSet
  "relatedArtifact" : [{ RelatedArtifact }], // Additional documentation, citations, etc
  "compose" : { // Content logical definition of the value set (CLD)
    "lockedDate" : "<date>", // Fixed date for references with no specified version (transitive)
    "inactive" : <boolean>, // Whether inactive codes are in the value set
    "include" : [{ // R!  Include one or more codes from a code system or other value set(s)
      "system" : "<uri>", // I The system the codes come from
      "version" : "<string>", // Specific version of the code system referred to
      "concept" : [{ // I A concept defined in the system
        "code" : "<code>", // R!  Code or expression from system
        "display" : "<string>", // Text to display for this code for this value set in this valueset
        "designation" : [{ // Additional representations for this concept
          "language" : "<code>", // Human language of the designation
          "use" : { Coding }, // I Types of uses of designations
          "additionalUse" : [{ Coding }], // I Additional ways how this designation would be used
          "value" : "<string>" // R!  The text value for this designation
        }]
      }],
      "filter" : [{ // I Select codes/concepts by their properties (including relationships)
        "property" : "<code>", // R!  A property/filter defined by the code system
        "op" : "<code>", // R!  = | is-a | descendent-of | is-not-a | regex | in | not-in | generalizes | child-of | descendent-leaf | exists
        "value" : "<string>" // R!  Code from the system, or regex criteria, or boolean value for exists
      }],
      "valueSet" : ["<canonical(ValueSet)>"], // I Select the contents included in this value set
      "copyright" : "<string>" // A copyright statement for the specific code system included in the value set
    }],
    "exclude" : [{ Content as for ValueSet.compose.include }], // Explicitly exclude codes from a code system or other value sets
    "property" : ["<string>"] // Property to return if client doesn't override
  },
  "expansion" : { // Used when the value set is "expanded"
    "identifier" : "<uri>", // Identifies the value set expansion (business identifier)
    "next" : "<uri>", // Opaque urls for paging through expansion results
    "timestamp" : "<dateTime>", // R!  Time ValueSet expansion happened
    "total" : <integer>, // Total number of codes in the expansion
    "offset" : <integer>, // Offset at which this resource starts
    "parameter" : [{ // Parameter that controlled the expansion process
      "name" : "<string>", // R!  Name as assigned by the client or server
      // value[x]: Value of the named parameter. One of these 7:
      "valueString" : "<string>",
      "valueBoolean" : <boolean>,
      "valueInteger" : <integer>,
      "valueDecimal" : <decimal>,
      "valueUri" : "<uri>",
      "valueCode" : "<code>",
      "valueDateTime" : "<dateTime>"
    }],
    "property" : [{ // Additional information supplied about each concept
      "code" : "<code>", // R!  Identifies the property on the concepts, and when referred to in operations
      "uri" : "<uri>" // Formal identifier for the property
    }],
    "contains" : [{ // Codes in the value set
      "system" : "<uri>", // I System value for the code
      "abstract" : <boolean>, // I If user cannot select this entry
      "inactive" : <boolean>, // If concept is inactive in the code system
      "version" : "<string>", // Version in which this code/display is defined
      "code" : "<code>", // I Code - if blank, this is not a selectable code
      "display" : "<string>", // I User display for the concept
      "designation" : [{ Content as for ValueSet.compose.include.concept.designation }], // Additional representations for this item
      "property" : [{ // Property value for the concept
        "code" : "<code>", // R!  Reference to ValueSet.expansion.property.code
        // value[x]: Value of the property for this concept. One of these 7:
        "valueCode" : "<code>",
        "valueCoding" : { Coding },
        "valueString" : "<string>",
        "valueInteger" : <integer>,
        "valueBoolean" : <boolean>,
        "valueDateTime" : "<dateTime>",
        "valueDecimal" : <decimal>,
        "subProperty" : [{ // SubProperty value for the concept
          "code" : "<code>", // R!  Reference to ValueSet.expansion.property.code
          // value[x]: Value of the subproperty for this concept. One of these 7:
          "valueCode" : "<code>",
          "valueCoding" : { Coding },
          "valueString" : "<string>",
          "valueInteger" : <integer>,
          "valueBoolean" : <boolean>,
          "valueDateTime" : "<dateTime>",
          "valueDecimal" : <decimal>
        }]
      }],
      "contains" : [{ Content as for ValueSet.expansion.contains }] // Codes contained under this entry
    }]
  },
  "scope" : { // Description of the semantic space the Value Set Expansion is intended to cover and should further clarify the text in ValueSet.description
    "inclusionCriteria" : "<string>", // Criteria describing which concepts or codes should be included and why
    "exclusionCriteria" : "<string>" // Criteria describing which concepts or codes should be excluded and why
  }
}
```