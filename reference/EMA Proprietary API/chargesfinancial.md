---
title: Charges/Financial
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
Base Profile: [https://www.hl7.org/fhir/chargeitem.html](https://www.hl7.org/fhir/chargeitem.html)

Common use cases include:

* Find Charges for a Patient
* Find Charges from an Encounter
* Add Charges to a Patient’s account

Modernizing Medicine has several different flavors of ChargeItem depending on each practice’s unique configuration.

* Practices which have EMA-only (no MMPM) will notice the following:
  * Charges are only available once an encounter is finalized
  * Charges cannot be created for these practices (since they do not have MMPM, you’re application should be sending charges to the practice’s PM system)
  * There are no INBOUND charges for these practices
  * All charges will reference an encounter in EMA as this is the only way to generate a ChargeItem.
* Practices which use MMPM as their PM system will notice the following:
  * INBOUND charges may be coming from other applications
  * Not all Charges will be associated to an encounter

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
        The unique ID for a ChargeItem
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        financialTransaction\*
      </td>

      <td style={{ textAlign: "left" }}>
        Custom Extension designed to replicate HL7 DFT
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        financialTransactionId
      </td>

      <td style={{ textAlign: "left" }}>
        ID of the transaction. This is not used for CREATE. One will be returned to you upon a CREATE.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        transactionStatus
      </td>

      <td style={{ textAlign: "left" }}>
        Charged|
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
         totalCost
      </td>

      <td style={{ textAlign: "left" }}>
        The totalCost of a financialTransaction if it cannot or will not be computed by other inputs.   

        valueMoney: currency USD
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        attendingProviderId
      </td>

      <td style={{ textAlign: "left" }}>
        Attending Provider NPI or PMSID Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        referralProviderId
      </td>

      <td style={{ textAlign: "left" }}>
        Referral Provider NPI or PMSID Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        locationId
      </td>

      <td style={{ textAlign: "left" }}>
        Location NPI or PMSID Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        businessUnitId
      </td>

      <td style={{ textAlign: "left" }}>
        Business Unit Id Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        transactionId
      </td>

      <td style={{ textAlign: "left" }}>
        Transaction Id Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        sendingFacility
      </td>

      <td style={{ textAlign: "left" }}>
        Global Code from MSH Header Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        receivingFacility
      </td>

      <td style={{ textAlign: "left" }}>
        Firm Code from MSH Header Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        financialTransactionDetail\*
      </td>

      <td style={{ textAlign: "left" }}>
        Custom Extension designed to replicate FT1 segment of an HL7 DFT   

        NOTE: You can add multiple financialTransactionDetail(s).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        financialTransactionDetailId
      </td>

      <td style={{ textAlign: "left" }}>
        ID of the transaction. This is not used for CREATE. One will be returned to you upon a CREATE. This will be used to support the READ in the future.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        transactionType
      </td>

      <td style={{ textAlign: "left" }}>
        CG - Charge is the only type supported at this time
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        performingProviderId
      </td>

      <td style={{ textAlign: "left" }}>
        Performing Provider NPI or PMSID Goes here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        CPT Code
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        unitCost
      </td>

      <td style={{ textAlign: "left" }}>
        valueMoney
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        quantity
      </td>

      <td style={{ textAlign: "left" }}>
        valueDecimal
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        description
      </td>

      <td style={{ textAlign: "left" }}>
        valueString
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        postingDate
      </td>

      <td style={{ textAlign: "left" }}>
        valueDateTime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        transactionPeriod
      </td>

      <td style={{ textAlign: "left" }}>
        valuePeriod
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        diagnosisDetail
      </td>

      <td style={{ textAlign: "left" }}>
        Custom Extension designed to replicate the DG1 segment of an HL7 DFT    

        NOTE: You can add multiple diagnosisDetail(s)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        diagnosisDetailId
      </td>

      <td style={{ textAlign: "left" }}>
        valueString\
        ID of the diagnosis. This is not used for CREATE. One will be returned to you upon a CREATE. This will be used to support the READ in the future.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        diagnosisDetailCode
      </td>

      <td style={{ textAlign: "left" }}>
        valueCoding\
        ICD-10 codes are supported at this time.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        procedureDetail\*
      </td>

      <td style={{ textAlign: "left" }}>
        Custom Extension designed to replicate FT1 segment of an HL7 DFT    

        NOTE: You can add multiple procedureDetail(s)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        procedureDetailId
      </td>

      <td style={{ textAlign: "left" }}>
        ID of the procedure. This is not used for CREATE. One will be returned to you upon a CREATE. This will be used to support the READ in the future.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        procedureCode
      </td>

      <td style={{ textAlign: "left" }}>
        valueCoding
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        anesthesiaCode
      </td>

      <td style={{ textAlign: "left" }}>
        valueCoding
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        anesthesiaMinutes
      </td>

      <td style={{ textAlign: "left" }}>
        valueString
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        anesthesiaProviderId
      </td>

      <td style={{ textAlign: "left" }}>
        valueString\
        Anesthesia Provider NPI Goes Here
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        procedureType
      </td>

      <td style={{ textAlign: "left" }}>
        valueString
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        procedureCodeModifier
      </td>

      <td style={{ textAlign: "left" }}>
        valueString\
        Procedure Charge Code Modifier Goes here\
        NOTE: You can add multiple procedureCodeModifier(s).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        planned | billable | not-billable | aborted | billed | entered-in-error | unknown    

        NOTE: Only ‘billable’ is supported at this time.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        occurrenceDateTime
      </td>

      <td style={{ textAlign: "left" }}>
        valueDateTime
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        Patient Reference
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        context
      </td>

      <td style={{ textAlign: "left" }}>
        Encounter ID (if known)\
        NOTE: This is to be built out in the next release.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reason
      </td>

      <td style={{ textAlign: "left" }}>
        valueCoding\
        NOTE: Only ICD-10 codes are supported at this time.
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* ChargeItem READ
* ChargeItem SEARCH
* ChargeItem CREATE

***

### ChargeItem READ

| HTTP Request                                                           | Method | Action                                       |
| :--------------------------------------------------------------------- | :----- | :------------------------------------------- |
| \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/ChargeItem                | GET    | Get All ChargeItems for a Practice           |
| \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/ChargeItem/CHG\|\{id}     | GET    | Get a specific ChargeItem                    |
| \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/ChargeItem/INBOUND        | GET    | Get all Inbound Charges for a Practice       |
| \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/ChargeItem/INBOUND\|\{id} | GET    | Get a specific inbound Charge for a Practice |

***

### ChargeItem CREATE

If your application is planning on sending charges into MMPM, this will require some additional setup and configuration. It is recommended that you speak with whomever provided you access to the MMI Sandbox.

* Practices which have EMA-only (no MMPM) will notice the following:
  * Charges are only available once an encounter is finalized
  * Charges cannot be created for these practices (since they do not have MMPM, you’re application should be sending charges to the practice’s PM system)
  * There are no INBOUND charges for these practices
  * All charges will reference an encounter in EMA as this is the only way to generate a ChargeItem.
* Practices which use MMPM as their PM system will notice the following:
  * INBOUND charges may be coming from other applications
  * Not all Charges will be associated to an encounter

When generating charges for a customer, here are a few things you’ll want to consider. First, if you pass in a ‘unitCost’ value, it will override the ‘Fee Schedule’ that the customer has configured for the particular CPT code. So, if you want to do that (which may be the case in some scenarios), be sure to pass it in. It will take the Quantity and multiply it by that value. If you do not know or want to use the Fee Schedule already configured for that CPT code, do not pass in ‘unitCost’ - that way it will simply default to what the customer has configured.

The ‘transactionID’ is something you would pass in that may mean something to you or your customer. It will appear in the UI and they can search on it if you need to reference it for any reason.

Some customers have a setting which automatically creates bills from Charges assuming the information needed is there.

Customers that use this functionality have an ‘Inbound Charges’ queue in their ‘Financials’ experience:

![](https://files.readme.io/896fd4e2e111abdfcd8fe6dc13a51fb22bb8a67a5d2b194111f4a856eff9d38f-image.png)

If they are Auto-creating bills from charges, you may want to instruct your customers to check the New Bills tab if they are looking for something they are expecting to be here.
