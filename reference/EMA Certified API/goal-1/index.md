---
title: Goal
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-goal](http://hl7.org/fhir/us/core/StructureDefinition/us-core-goal)

The FHIR (Fast Healthcare Interoperability Resources) Goal resource is used to define specific goals for a patient, such as treatment goals, behavioral change goals, or other types of health-related objectives. The Goal endpoint in an FHIR API allows clients to retrieve and manage these goals.

### Key Components of a FHIR Goal Resource

1. **id**: Unique identifier for the goal.
2. **meta**: Metadata about the resource, including version, last updated time, etc.
3. **status**: Indicates the current status of the goal (e.g., proposed, accepted, planned, in-progress, on-target, ahead-of-target, behind-target, suspended, cancelled, completed, entered-in-error, rejected).
4. **description**: A detailed description of the goal, often in natural language.
5. **subject**: Reference to the patient or other entity to whom this goal is associated.
6. **startDate**: The date when the goal was defined.
7. **target**: Sub-component that specifies target outcomes, dates, and other measures.
8. **category**: Categorical descriptor for the goal (e.g., dietary, behavioral, etc.).
9. **priority**: The priority of the goal (e.g., high-priority, medium-priority).
10. **addresses**: References to conditions/problem statements/issues being addressed by the goal.
11. **note**: Comments or notes about the goal.

**Sample Response Object:**

```Text json
{  
  "resourceType": "Goal",  
  "id": "example",  
  "status": "in-progress",  
  "description": {  
    "text": "Achieve a weight loss of 10 kg over the next 6 months"  
  },  
  "subject": {  
    "reference": "Patient/12345",  
    "display": "John Doe"  
  },  
  "startDate": "2023-01-01",  
  "target": \[  
    {  
      "measure": {  
        "coding": [  
          {  
            "system": "http://loinc.org",  
            "code": "29463-7",  
            "display": "Body Weight"  
          }  
        ],  
        "text": "Body Weight"  
      },  
      "detailQuantity": {  
        "value": 70,  
        "unit": "kg",  
        "system": "<http://unitsofmeasure.org">,  
        "code": "kg"  
      },  
      "dueDate": "2023-07-01"  
    }  
  ],  
  "category": \[  
    {  
      "coding": [  
        {  
          "system": "http://hl7.org/fhir/goal-category",  
          "code": "dietary",  
          "display": "Dietary"  
        }  
      ]  
    }  
  ],  
  "priority": {  
    "coding": [  
      {  
        "system": "http://hl7.org/fhir/goal-priority",  
        "code": "high-priority",  
        "display": "High Priority"  
      }  
    ]  
  },  
  "addresses": [  
    {  
      "reference": "Condition/67890",  
      "display": "Obesity"  
    }  
  ],  
  "note": [  
    {  
      "text": "Patient is motivated and has strong family support."  
    }  
  ]  
}
```

This example provides a comprehensive look at a single goal resource, specifying a patient's goal to achieve a particular weight by a specific date, along with other relevant details.
