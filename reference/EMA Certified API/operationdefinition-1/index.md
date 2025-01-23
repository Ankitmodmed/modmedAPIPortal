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

The OperationDefinition resource defines the parameters and overall definition of a specific operation or named query for FHIR.\
An OperationDefinition endpoint describes the characteristics, parameters, and responses for a specific operation. Below is an illustrative example of what an OperationDefinition might look like and its key components.

## Key Components

* **resourceType**: The type of resource, which is OperationDefinition in this case.
* **id**: Unique identifier for the OperationDefinition.
* **url**: Canonical URL for the OperationDefinition.
* **version**: Version of the operation definition.
* **name**: The name of the operation.
* **status**: Status of the operation definition (e.g., draft, active).
* **kind**: Specifies that this resource is an operation.
* **date**: The date this version of the operation definition was published.
* **publisher**: Organization or individual responsible for the publication.
* **description**: Human-readable description of the operation.
* **code**: The identifier code used to invoke the operation.
* **resource**: The list of resource types that this operation can be used with (e.g., Patient).
* **system**: Boolean indicating if this operation can work at the system level.
* **type**: Boolean value indicating if this operation can be invoked for individual resources.
* **instance**: Boolean value indicating if this operation can be invoked on instances.
* **parameter**: Describes the input and output parameters for the operation. Each parameter has:
* **name**: Name of the parameter.
* **use**: Direction of the parameter (either in or out).
* **min/max**: Minimum and maximum number of times the parameter can appear.
* **documentation**: Description of the parameter.
* **type**: Data type of the parameter (e.g., string, OperationOutcome).

<br />

New content:

The OperationDefinition resource provides a formal computable definition of an operation(on the RESTful interface) or a named query(using the search interaction).

Read more from: [https://hl7.org/fhir/operationdefinition.html](https://hl7.org/fhir/operationdefinition.html)

<br />

**Sample Response Object:**

```Text json
{  
  "resourceType": "OperationDefinition",  
  "id": "example",  
  "url": "<http://example.org/fhir/OperationDefinition/example">,  
  "version": "1.0.0",  
  "name": "ExampleOperation",  
  "status": "draft",  
  "kind": "operation",  
  "date": "2023-10-06T12:00:00Z",  
  "publisher": "Example Publisher",  
  "description": "An example operation definition.",  
  "code": "example",  
  "resource": [  
    "Patient"  
  ],  
  "system": false,  
  "type": true,  
  "instance": true,  
  "parameter": [  
    {  
      "name": "exampleParameter",  
      "use": "in",  
      "min": 1,  
      "max": "1",  
      "documentation": "An example input parameter.",  
      "type": "string"  
    },  
    {  
      "name": "return",  
      "use": "out",  
      "min": 1,  
      "max": "1",  
      "documentation": "An example return value.",  
      "type": "OperationOutcome"  
    }  
  ]  
}
```
```json new json
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