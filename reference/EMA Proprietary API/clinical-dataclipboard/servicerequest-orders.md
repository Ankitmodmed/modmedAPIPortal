---
title: ServiceRequest (Orders)
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
Base profile: <https://www.hl7.org/fhir/servicerequest.html>

The **ServiceRequest** resource can be used to retrieve any order that can be electronically ordered within EMA. This resource can be configured in various ways depending on the use case.

**Common Use Cases:**

1. **Vendor-Specific Orders:**  
   A typical use case is when a vendor only needs to be notified of new orders specific to them. For example, in the case of lab orders, a practice may send orders to multiple labs (e.g., Lab A and Lab B). In this scenario, Lab A only needs to see orders meant for them and should not be aware of orders sent to Lab B. To facilitate this, the system can be configured so that when the vendor queries the **ServiceRequest** resource, they will only see orders where they are the selected performer.
2. **All Orders:**  
   Some vendors may need to be aware of all orders, regardless of where they are performed. For these vendors, the system can be configured to allow access to all **ServiceRequests**, not limited to specific performers.

**Configuration Notes:**

- It's important to inform **ModMed Integration (MMI)** of your specific needs so the correct configuration can be applied.
- By default, when you are provisioned a generic sandbox, you will likely have access to view **all ServiceRequests **unless you explicitly request a vendor-specific setup.

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "",
    "1-0": "lastUpdated",
    "1-1": "",
    "2-0": "basedOn",
    "2-1": "RequestGroup Reference",
    "3-0": "requisition",
    "3-1": "string - the requisition (order) number in EMA",
    "4-0": "status",
    "4-1": "draft, active, closed",
    "5-0": "intent",
    "5-1": "order",
    "6-0": "category",
    "6-1": "Type of Order - ValueSet/service-request-category-type  \nCurrent supported types:  \n  \n- Surgical\n- Therapies\n- Radiology",
    "7-0": "priority",
    "7-1": "",
    "8-0": "code",
    "8-1": "Orderable Code - likely CPT, LOINC, or Compendium code",
    "9-0": "subject",
    "9-1": "Reference to Encounter",
    "10-0": "occurrenceDateTime",
    "10-1": "",
    "11-0": "authoredOn",
    "11-1": "datetime",
    "12-0": "requester",
    "12-1": "Reference to Practitioner",
    "13-0": "reasonCode",
    "13-1": "Typically an ICD10 diagnosis",
    "14-0": "insurance",
    "14-1": "Reference to Coverage",
    "15-0": "bodySite",
    "15-1": "If the practitioner selected a body location in EMA, that will appear here",
    "16-0": "note",
    "16-1": "Additional clinically relevant data",
    "17-0": "supportingInfo",
    "17-1": "Reference to the Order PDF Document"
  },
  "cols": 2,
  "rows": 18,
  "align": [
    "left",
    "left"
  ]
}
[/block]