---
title: Clinical Data/Clipboard
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
MMI has developed functionality that allows 3rd party vendors to send structured data to the Clipboard. Currently, only Problem List, Medications, and Allergies are supported. However, we will be adding support for other elements of the clipboard in the near future.

## **User Experience**

When a vendor POSTs something new to a Patient, an EMA user will see a modal pop up the next time\
they visit that Patient’s chart:

<Image align="center" src="https://files.readme.io/28bdf52bd934d4d2899569008a27aafade1817c78c97609ac70d3d54100034f0-image.png" />

From there, any of the new items can either be individually reconciled or all can be accepted or rejected\
at once:

![](https://files.readme.io/11f01d3e651a87900b8b6f7fde1f64a7d6fdd42c35c6904d597cdef0ba0983be-image.png)

The following sections of the clipboard can be updated and a sample payload is provided for each type:

### **Problem List**

```Text json
{
  "resourceType": "Condition",
  "clinicalStatus": {
    "coding": [
      {
        "system": "http://hl7.org/fhir/ValueSet/condition-clinical",
        "code": "ACTIVE",
        "display": "Active"
      }
    ],
    "text": "Active"
  },
  "category": [
    {
      "coding": [
        {
          "system": "{base url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/condition-category",
          "code": "DIAGNOSIS",
          "display": "Diagnosis"
        }
      ],
      "text": "Diagnosis"
    }
  ],
  "code": {
    "coding": [
      {
        "system": "ICD10",
        "code": "F41.9",
        "display": "Anxiety Disorder, Unspecified"
      }
    ],
    "text": "Anxiety Disorder, Unspecified"
  },
  "subject": {
    "reference": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/23715679",
    "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/23715679"
  },
  "onsetDateTime": "2020-02-14T10:21:14+00:00",
  "recordedDate": "2020-02-14T15:21:14+00:00"
}
```

### **Allergies**

```Text json
{
  "resourceType": "AllergyIntolerance",
  "clinicalStatus": {
    "coding": [
      {
        "system": "https://www.hl7.org/fhir/valueset-allergyintolerance-clinical.html",
        "code": "active",
        "display": "Active"
      }
    ],
    "text": "Active"
  },
  "code": {
    "coding": [
      {
        "system": "RxNorm",
        "code": "211874",
        "display": "Bayer Aspirin"
      }
    ],
    "text": "Bayer Aspirin"
  },
  "patient": {
    "reference": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/23715679",
    "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/23715679"
  },
  "onsetDateTime": "2024-05-06T00:00:00+00:00",
  "recordedDate": "2024-05-06T00:00:00+00:00",
  "reaction": [
    {
      "substance": {
        "coding": [
          {
            "system": "RxNorm",
            "code": "211874",
            "display": "Bayer Aspirin"
          }
        ],
        "text": "Bayer Aspirin"
      },
      "manifestation": [
        {
          "coding": [
            {
              "system": "SNOMED CT",
              "code": "422587007",
              "display": "Nausea"
            }
          ],
          "text": "Nausea"
        }
      ],
      "description": "Nausea"
    }
  ]
}
```

### **Medications**

```Text json
{
  "resourceType": "MedicationStatement",
  "status": "active",
  "medicationCodeableConcept": {
    "coding": [
      {
        "system": "RxNorm",
        "code": "209387",
        "display": "Tylenol"
      }
    ],
    "text": "Tylenol"
  },
  "subject": {
    "reference": "{base url}/{firm_url_prefix}/Patient/73337",
    "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/73337"
  },
  "dosage": [
    {
      "route": {
        "coding": [
          {
            "system": "FDA RouteOfAdministration",
            "code": "C38288",
            "display": "ORAL"
          }
        ],
        "text": "ORAL"
      },
      "doseAndRate": [
        {
          "doseQuantity": {
            "value": 325
          }
        }
      ]
    }
  ]
}
```
