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
Base profile: <http://hl7.org/fhir/StructureDefinition/OperationDefinition>

The OperationDefinition resource defines the parameters and overall definition of a specific operation or named query for FHIR.  
An OperationDefinition endpoint describes the characteristics, parameters, and responses for a specific operation. Below is an illustrative example of what an OperationDefinition might look like and its key components.

## Key Components

- **resourceType**: The type of resource, which is OperationDefinition in this case.
- **id**: Unique identifier for the OperationDefinition.
- **url**: Canonical URL for the OperationDefinition.
- **version**: Version of the operation definition.
- **name**: The name of the operation.
- **status**: Status of the operation definition (e.g., draft, active).
- **kind**: Specifies that this resource is an operation.
- **date**: The date this version of the operation definition was published.
- **publisher**: Organization or individual responsible for the publication.
- **description**: Human-readable description of the operation.
- **code**: The identifier code used to invoke the operation.
- **resource**: The list of resource types that this operation can be used with (e.g., Patient).
- **system**: Boolean indicating if this operation can work at the system level.
- **type**: Boolean value indicating if this operation can be invoked for individual resources.
- **instance**: Boolean value indicating if this operation can be invoked on instances.
- **parameter**: Describes the input and output parameters for the operation. Each parameter has:
- **name**: Name of the parameter.
- **use**: Direction of the parameter (either in or out).
- **min/max**: Minimum and maximum number of times the parameter can appear.
- **documentation**: Description of the parameter.
- **type**: Data type of the parameter (e.g., string, OperationOutcome).

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