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
Base profile: [https://www.hl7.org/fhir/servicerequest.html](https://www.hl7.org/fhir/servicerequest.html)

The **ServiceRequest** resource can be used to retrieve any order that can be electronically ordered within EMA. This resource can be configured in various ways depending on the use case.

**Common Use Cases:**

1. **Vendor-Specific Orders:**\
   A typical use case is when a vendor only needs to be notified of new orders specific to them. For example, in the case of lab orders, a practice may send orders to multiple labs (e.g., Lab A and Lab B). In this scenario, Lab A only needs to see orders meant for them and should not be aware of orders sent to Lab B. To facilitate this, the system can be configured so that when the vendor queries the **ServiceRequest** resource, they will only see orders where they are the selected performer.
2. **All Orders:**\
   Some vendors may need to be aware of all orders, regardless of where they are performed. For these vendors, the system can be configured to allow access to all **ServiceRequests**, not limited to specific performers.

**Configuration Notes:**

* It's important to inform **ModMed Integration (MMI)** of your specific needs so the correct configuration can be applied.
* By default, when you are provisioned a generic sandbox, you will likely have access to view **all ServiceRequests** unless you explicitly request a vendor-specific setup.

The following attributes are supported:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Field Name
      </th>

      <th style={{ textAlign: "left" }}>
        Notes
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        id
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        lastUpdated
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        basedOn
      </td>

      <td style={{ textAlign: "left" }}>
        RequestGroup Reference
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        requisition
      </td>

      <td style={{ textAlign: "left" }}>
        string - the requisition (order) number in EMA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        draft, active, closed
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        intent
      </td>

      <td style={{ textAlign: "left" }}>
        order
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        category
      </td>

      <td style={{ textAlign: "left" }}>
        Type of Order - ValueSet/service-request-category-type\
        Current supported types:  

        * Surgical
        * Therapies
        * Radiology
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        priority
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        Orderable Code - likely CPT, LOINC, or Compendium code
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Encounter
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        occurrenceDateTime
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        authoredOn
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        requester
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Practitioner
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reasonCode
      </td>

      <td style={{ textAlign: "left" }}>
        Typically an ICD10 diagnosis
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        insurance
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Coverage
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        bodySite
      </td>

      <td style={{ textAlign: "left" }}>
        If the practitioner selected a body location in EMA, that will appear here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        note
      </td>

      <td style={{ textAlign: "left" }}>
        Additional clinically relevant data
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        supportingInfo
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to the Order PDF Document
      </td>
    </tr>
  </tbody>
</Table>