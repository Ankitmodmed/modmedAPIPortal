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
Base profile: <http://hl7.org/fhir/us/core/StructureDefinition/us-core-coverage>

Coverage typically refers to insurance information about a patient, such as the health plan, subscriber, and characteristics of the coverage.  
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

These components offer detailed information about the insurance coverage for clinical and administrative purposes.