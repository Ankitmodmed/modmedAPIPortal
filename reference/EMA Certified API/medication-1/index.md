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

The Medication endpoint in FHIR is used to represent a medication that can be or is being dispensed or administered to a patient.\
Here are some key components of the FHIR Medication resource:

* **Id**: Unique identifier for the medication resource.
* **Code**: A code (or set of codes) that specify a particular medication.
* **Status**: The status of the medication (active, inactive, etc.).
* **Manufacturer**: Information about the manufacturer of the medication.
* **Form**: The form in which the medication is administered (tablet, injection, etc.).
* **Ingredient**: Details about the ingredient(s) in the medication.
* **Batch**: Information about the batch of the medication (if applicable).

<br />

New content:

Medication resource is primarily used for the identification and definition of a medication, including ingredients, for the purposes of prescribing, dispensing, and administering a medication as well as for making statements about medication use.

Read more from: [https://hl7.org/fhir/medication.html](https://hl7.org/fhir/medication.html)

<br />

**Sample Response Object:**

```Text json
{
  "resourceType": "Medication",
  "id": "medication-example",
  "code": {
    "coding": [
      {
        "system": "http://www.nlm.nih.gov/research/umls/rxnorm",
        "code": "313782",
        "display": "Aspirin 81 MG Oral Tablet"
      }
    ],
    "text": "Aspirin 81 MG Oral Tablet"
  },
  "status": "active",
  "manufacturer": {
    "reference": "Organization/example",
    "display": "ExamplePharma"
  },
  "form": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "385055001",
        "display": "Tablet dose form"
      }
    ],
    "text": "Tablet"
  },
  "ingredient": [
    {
      "itemCodeableConcept": {
        "coding": [
          {
            "system": "http://www.nlm.nih.gov/research/umls/rxnorm",
            "code": "1191",
            "display": "Aspirin"
          }
        ],
        "text": "Aspirin"
      },
      "isActive": true,
      "strength": {
        "numerator": {
          "value": 81,
          "unit": "mg",
          "system": "http://unitsofmeasure.org",
          "code": "mg"
        },
        "denominator": {
          "value": 1,
          "unit": "tab",
          "system": "http://unitsofmeasure.org",
          "code": "tab"
        }
      }
    }
  ],
  "batch": {
    "lotNumber": "12345",
    "expirationDate": "2022-10-31"
  }
}
```
```json new json
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