---
title: OperationDefinition
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
Base profile: [http://hl7.org/fhir/StructureDefinition/OperationDefinition](http://hl7.org/fhir/StructureDefinition/OperationDefinition)

The OperationDefinition resource provides a formal computable definition of an operation(on the RESTful interface) or a named query(using the search interaction).

Read more from: [https://hl7.org/fhir/operationdefinition.html](https://hl7.org/fhir/operationdefinition.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "OperationDefinition",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "url" : "<uri>", // Canonical identifier for this operation definition, represented as an absolute URI (globally unique)
  "identifier" : [{ Identifier }], // Additional identifier for the implementation guide (business identifier)
  "version" : "<string>", // Business version of the operation definition
  // versionAlgorithm[x]: How to compare versions. One of these 2:
  "versionAlgorithmString" : "<string>",
  "versionAlgorithmCoding" : { Coding },
  "name" : "<string>", // I R!  Name for this operation definition (computer friendly)
  "title" : "<string>", // Name for this operation definition (human friendly)
  "status" : "<code>", // R!  draft | active | retired | unknown
  "kind" : "<code>", // I R!  operation | query
  "experimental" : <boolean>, // For testing purposes, not real usage
  "date" : "<dateTime>", // Date last changed
  "publisher" : "<string>", // Name of the publisher/steward (organization or individual)
  "contact" : [{ ContactDetail }], // Contact details for the publisher
  "description" : "<markdown>", // Natural language description of the operation definition
  "useContext" : [{ UsageContext }], // The context that the content is intended to support
  "jurisdiction" : [{ CodeableConcept }], // Intended jurisdiction for operation definition (if applicable)
  "purpose" : "<markdown>", // Why this operation definition is defined
  "copyright" : "<markdown>", // Use and/or publishing restrictions
  "copyrightLabel" : "<string>", // Copyright holder and year(s)
  "affectsState" : <boolean>, // Whether content is changed by the operation
  "code" : "<code>", // R!  Recommended name for operation in search url
  "comment" : "<markdown>", // Additional information about use
  "base" : "<canonical(OperationDefinition)>", // Marks this as a profile of the base
  "resource" : ["<code>"], // Types this operation applies to
  "system" : <boolean>, // R!  Invoke at the system level?
  "type" : <boolean>, // R!  Invoke at the type level?
  "instance" : <boolean>, // I R!  Invoke on an instance?
  "inputProfile" : "<canonical(StructureDefinition)>", // Validation information for in parameters
  "outputProfile" : "<canonical(StructureDefinition)>", // Validation information for out parameters
  "parameter" : [{ // I Parameters for the operation/query
    "name" : "<code>", // I R!  Name in Parameters.parameter.name or in URL
    "use" : "<code>", // I R!  in | out
    "scope" : ["<code>"], // instance | type | system
    "min" : <integer>, // R!  Minimum Cardinality
    "max" : "<string>", // R!  Maximum Cardinality (a number or *)
    "documentation" : "<markdown>", // Description of meaning/use
    "type" : "<code>", // I What type this parameter has
    "allowedType" : ["<code>"], // Allowed sub-type this parameter can have (if type is abstract)
    "targetProfile" : ["<canonical(StructureDefinition)>"], // I If type is Reference | canonical, allowed targets. If type is 'Resource', then this constrains the allowed resource types
    "searchType" : "<code>", // I number | date | string | token | reference | composite | quantity | uri | special
    "binding" : { // ValueSet details if this is coded
      "strength" : "<code>", // R!  required | extensible | preferred | example
      "valueSet" : "<canonical(ValueSet)>" // R!  Source of value set
    },
    "referencedFrom" : [{ // References to this parameter
      "source" : "<string>", // R!  Referencing parameter
      "sourceId" : "<string>" // Element id of reference
    }],
    "part" : [{ Content as for OperationDefinition.parameter }] // I Parts of a nested Parameter
  }],
  "overload" : [{ // Define overloaded variants for when  generating code
    "parameterName" : ["<string>"], // Name of parameter to include in overload
    "comment" : "<string>" // Comments to go on overload
  }]
}
```