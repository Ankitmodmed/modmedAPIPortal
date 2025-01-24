---
title: Medication
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
Base profile: [http://hl7.org/fhir/StructureDefinition/Medication](http://hl7.org/fhir/StructureDefinition/Medication)

Medication resource is primarily used for the identification and definition of a medication, including ingredients, for the purposes of prescribing, dispensing, and administering a medication as well as for making statements about medication use.

Read more from: [https://hl7.org/fhir/medication.html](https://hl7.org/fhir/medication.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "Medication",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business identifier for this medication
  "code" : { CodeableConcept }, // Codes that identify this medication
  "status" : "<code>", // active | inactive | entered-in-error
  "marketingAuthorizationHolder" : { Reference(Organization) }, // Organization that has authorization to market medication
  "doseForm" : { CodeableConcept }, // powder | tablets | capsule +
  "totalVolume" : { Quantity }, // When the specified product code does not infer a package size, this is the specific amount of drug in the product
  "ingredient" : [{ // Active or inactive ingredient
    "item" : { CodeableReference(Medication|Substance) }, // R!  The ingredient (substance or medication) that the ingredient.strength relates to
    "isActive" : <boolean>, // Active ingredient indicator
    // strength[x]: Quantity of ingredient present. One of these 3:
    "strengthRatio" : { Ratio },
    "strengthCodeableConcept" : { CodeableConcept },
    "strengthQuantity" : { Quantity }
  }],
  "batch" : { // Details about packaged medications
    "lotNumber" : "<string>", // Identifier assigned to batch
    "expirationDate" : "<dateTime>" // When batch will expire
  },
  "definition" : { Reference(MedicationKnowledge) } // Knowledge about this medication
}
```