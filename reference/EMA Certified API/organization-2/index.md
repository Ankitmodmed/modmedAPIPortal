---
title: Organization
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-organization](http://hl7.org/fhir/us/core/StructureDefinition/us-core-organization)

The Organization resource is used for collections of people that have come together to achieve an objective.It often exists as a hierarchy of organization resources, using the part-of property to provide the association of the child to its parent organization.

Read more from: [https://hl7.org/fhir/R4/organization.html](https://hl7.org/fhir/R4/organization.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "Organization",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // C? Identifies this organization  across multiple systems
  "active" : <boolean>, // Whether the organization's record is still in active use
  "type" : [{ CodeableConcept }], // Kind of organization
  "name" : "<string>", // C? Name used for the organization
  "alias" : ["<string>"], // A list of alternate names that the organization is known as, or was known as in the past
  "telecom" : [{ ContactPoint }], // C? A contact detail for the organization
  "address" : [{ Address }], // C? An address for the organization
  "partOf" : { Reference(Organization) }, // The organization of which this organization forms a part
  "contact" : [{ // Contact for the organization for a certain purpose
    "purpose" : { CodeableConcept }, // The type of contact
    "name" : { HumanName }, // A name associated with the contact
    "telecom" : [{ ContactPoint }], // Contact details (telephone, email, etc.)  for a contact
    "address" : { Address } // Visiting or postal addresses for the contact
  }],
  "endpoint" : [{ Reference(Endpoint) }] // Technical endpoints providing access to services operated for the organization
}
```