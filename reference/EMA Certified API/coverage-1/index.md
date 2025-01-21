---
title: Coverage
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-coverage](http://hl7.org/fhir/us/core/StructureDefinition/us-core-coverage)

Coverage typically refers to insurance information about a patient, such as the health plan, subscriber, and characteristics of the coverage.\
Here are key components of the Coverage resource in FHIR:

1. **Identifier**: Unique identifiers assigned to the coverage.
2. **Status**: The status of the coverage (e.g., active, cancelled).
3. **SubscriberId**: Identifier of the subscriber (the person who holds the insurance policy).
4. **Beneficiary**: Reference to the patient who is covered.
5. **Payor**: Organization or individual responsible for payment.
6. **PolicyHolder**: The person named on the policy.
7. **Class**: Sub-categories of the coverage, such as plan, subclass etc.
8. **Network**: The network within which the coverage is applicable.
9. **Order**: The order of applicability if multiple coverages exist.
10. **Period**: The time period during which the coverage is in effect.

<br />

New content:

The Coverage resource provides key identifiers and details of an insurance plan, similar to information on an insurance card, used to cover health care costs. It can also register "SelfPay," where an individual or organization, not an insurer, assumes payment responsibility, distinct from being a guarantor of the patient’s account.

Read more from : [https://hl7.org/fhir/R4/coverage.html](https://hl7.org/fhir/R4/coverage.html)

<br />

**Sample Response Object:**

```Text json
{  
  "resourceType": "Coverage",  
  "id": "12345",  
  "status": "active",  
  "subscriberId": "A1234567890",  
  "beneficiary": {  
    "reference": "Patient/67890"  
  },  
  "payor": [  
    {  
      "reference": "Organization/1234"  
    }  
  ],  
  "policyHolder": {  
    "reference": "Patient/67890"  
  },  
  "class": [  
    {  
      "type": {  
        "code": "plan",  
        "display": "Plan"  
      },  
      "value": "PPO"  
    }  
  ],  
  "network": "NetworkName",  
  "order": 1,  
  "period": {  
    "start": "2023-01-01",  
    "end": "2023-12-31"  
  }  
}
```
```json new json
{
  "resourceType" : "Coverage",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business Identifier for the coverage
  "status" : "<code>", // R!  active | cancelled | draft | entered-in-error
  "type" : { CodeableConcept }, // Coverage category such as medical or accident
  "policyHolder" : { Reference(Patient|RelatedPerson|Organization) }, // Owner of the policy
  "subscriber" : { Reference(Patient|RelatedPerson) }, // Subscriber to the policy
  "subscriberId" : "<string>", // ID assigned to the subscriber
  "beneficiary" : { Reference(Patient) }, // R!  Plan beneficiary
  "dependent" : "<string>", // Dependent number
  "relationship" : { CodeableConcept }, // Beneficiary relationship to the subscriber
  "period" : { Period }, // Coverage start and end dates
  "payor" : [{ Reference(Organization|Patient|RelatedPerson) }], // R!  Issuer of the policy
  "class" : [{ // Additional coverage classifications
    "type" : { CodeableConcept }, // R!  Type of class such as 'group' or 'plan'
    "value" : "<string>", // R!  Value associated with the type
    "name" : "<string>" // Human readable description of the type and value
  }],
  "order" : "<positiveInt>", // Relative order of the coverage
  "network" : "<string>", // Insurer network
  "costToBeneficiary" : [{ // Patient payments for services/products
    "type" : { CodeableConcept }, // Cost category
    // value[x]: The amount or percentage due from the beneficiary. One of these 2:
    "valueQuantity" : { Quantity(SimpleQuantity) },
    "valueMoney" : { Money },
    "exception" : [{ // Exceptions for patient payments
      "type" : { CodeableConcept }, // R!  Exception category
      "period" : { Period } // The effective period of the exception
    }]
  }],
  "subrogation" : <boolean>, // Reimbursement to insurer
  "contract" : [{ Reference(Contract) }] // Contract details
}
```

These components offer detailed information about the insurance coverage for clinical and administrative purposes.