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
Base Profile: <https://www.hl7.org/fhir/chargeitem.html>

Common use cases include:

- Find Charges for a Patient
- Find Charges from an Encounter
- Add Charges to a Patient’s account

Modernizing Medicine has several different flavors of ChargeItem depending on each practice’s unique configuration.

- Practices which have EMA-only (no MMPM) will notice the following:
  - Charges are only available once an encounter is finalized
  - Charges cannot be created for these practices (since they do not have MMPM, you’re application should be sending charges to the practice’s PM system)
  - There are no INBOUND charges for these practices
  - All charges will reference an encounter in EMA as this is the only way to generate a ChargeItem.
- Practices which use MMPM as their PM system will notice the following:
  - INBOUND charges may be coming from other applications
  - Not all Charges will be associated to an encounter

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The unique ID for a ChargeItem",
    "1-0": "financialTransaction\\*",
    "1-1": "Custom Extension designed to replicate HL7 DFT",
    "2-0": "financialTransactionId",
    "2-1": "ID of the transaction. This is not used for CREATE. One will be returned to you upon a CREATE.",
    "3-0": "transactionStatus",
    "3-1": "Charged|",
    "4-0": " totalCost",
    "4-1": "The totalCost of a financialTransaction if it cannot or will not be computed by other inputs.   \n  \nvalueMoney: currency USD",
    "5-0": "attendingProviderId",
    "5-1": "Attending Provider NPI or PMSID Goes here",
    "6-0": "referralProviderId",
    "6-1": "Referral Provider NPI or PMSID Goes here",
    "7-0": "locationId",
    "7-1": "Location NPI or PMSID Goes here",
    "8-0": "businessUnitId",
    "8-1": "Business Unit Id Goes here",
    "9-0": "transactionId",
    "9-1": "Transaction Id Goes here",
    "10-0": "sendingFacility",
    "10-1": "Global Code from MSH Header Goes here",
    "11-0": "receivingFacility",
    "11-1": "Firm Code from MSH Header Goes here",
    "12-0": "financialTransactionDetail\\*",
    "12-1": "Custom Extension designed to replicate FT1 segment of an HL7 DFT   \n  \nNOTE: You can add multiple financialTransactionDetail(s).",
    "13-0": "financialTransactionDetailId",
    "13-1": "ID of the transaction. This is not used for CREATE. One will be returned to you upon a CREATE. This will be used to support the READ in the future.",
    "14-0": "transactionType",
    "14-1": "CG - Charge is the only type supported at this time",
    "15-0": "performingProviderId",
    "15-1": "Performing Provider NPI or PMSID Goes here",
    "16-0": "code",
    "16-1": "CPT Code",
    "17-0": "unitCost",
    "17-1": "valueMoney",
    "18-0": "quantity",
    "18-1": "valueDecimal",
    "19-0": "description",
    "19-1": "valueString",
    "20-0": "postingDate",
    "20-1": "valueDateTime",
    "21-0": "transactionPeriod",
    "21-1": "valuePeriod",
    "22-0": "diagnosisDetail",
    "22-1": "Custom Extension designed to replicate the DG1 segment of an HL7 DFT    \n  \nNOTE: You can add multiple diagnosisDetail(s)",
    "23-0": "diagnosisDetailId",
    "23-1": "valueString  \nID of the diagnosis. This is not used for CREATE. One will be returned to you upon a CREATE. This will be used to support the READ in the future.",
    "24-0": "diagnosisDetailCode",
    "24-1": "valueCoding  \nICD-10 codes are supported at this time.",
    "25-0": "procedureDetail\\*",
    "25-1": "Custom Extension designed to replicate FT1 segment of an HL7 DFT    \n  \nNOTE: You can add multiple procedureDetail(s)",
    "26-0": "procedureDetailId",
    "26-1": "ID of the procedure. This is not used for CREATE. One will be returned to you upon a CREATE. This will be used to support the READ in the future.",
    "27-0": "procedureCode",
    "27-1": "valueCoding",
    "28-0": "anesthesiaCode",
    "28-1": "valueCoding",
    "29-0": "anesthesiaMinutes",
    "29-1": "valueString",
    "30-0": "anesthesiaProviderId",
    "30-1": "valueString  \nAnesthesia Provider NPI Goes Here",
    "31-0": "procedureType",
    "31-1": "valueString",
    "32-0": "procedureCodeModifier",
    "32-1": "valueString  \nProcedure Charge Code Modifier Goes here  \nNOTE: You can add multiple procedureCodeModifier(s).",
    "33-0": "status",
    "33-1": "planned | billable | not-billable | aborted | billed | entered-in-error | unknown    \n  \nNOTE: Only ‘billable’ is supported at this time.",
    "34-0": "occurrenceDateTime",
    "34-1": "valueDateTime",
    "35-0": "subject",
    "35-1": "Patient Reference",
    "36-0": "context",
    "36-1": "Encounter ID (if known)  \nNOTE: This is to be built out in the next release.",
    "37-0": "reason",
    "37-1": "valueCoding  \nNOTE: Only ICD-10 codes are supported at this time."
  },
  "cols": 2,
  "rows": 38,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- ChargeItem READ
- ChargeItem SEARCH
- ChargeItem CREATE

***

### ChargeItem READ

| HTTP Request                                                      | Method | Action                                       |
| :---------------------------------------------------------------- | :----- | :------------------------------------------- |
| {base url}/{firm_url_prefix}/ema/fhir/v2/ChargeItem               | GET    | Get All ChargeItems for a Practice           |
| {base url}/{firm_url_prefix}/ema/fhir/v2/ChargeItem/CHG\|{id}     | GET    | Get a specific ChargeItem                    |
| {base url}/{firm_url_prefix}/ema/fhir/v2/ChargeItem/INBOUND       | GET    | Get all Inbound Charges for a Practice       |
| {base url}/{firm_url_prefix}/ema/fhir/v2/ChargeItem/INBOUND\|{id} | GET    | Get a specific inbound Charge for a Practice |

***

### ChargeItem CREATE

If your application is planning on sending charges into MMPM, this will require some additional setup and configuration. It is recommended that you speak with whomever provided you access to the MMI Sandbox.

- Practices which have EMA-only (no MMPM) will notice the following:
  - Charges are only available once an encounter is finalized
  - Charges cannot be created for these practices (since they do not have MMPM, you’re application should be sending charges to the practice’s PM system)
  - There are no INBOUND charges for these practices
  - All charges will reference an encounter in EMA as this is the only way to generate a ChargeItem.
- Practices which use MMPM as their PM system will notice the following:
  - INBOUND charges may be coming from other applications
  - Not all Charges will be associated to an encounter

When generating charges for a customer, here are a few things you’ll want to consider. First, if you pass in a ‘unitCost’ value, it will override the ‘Fee Schedule’ that the customer has configured for the particular CPT code. So, if you want to do that (which may be the case in some scenarios), be sure to pass it in. It will take the Quantity and multiply it by that value. If you do not know or want to use the Fee Schedule already configured for that CPT code, do not pass in ‘unitCost’ - that way it will simply default to what the customer has configured.

The ‘transactionID’ is something you would pass in that may mean something to you or your customer. It will appear in the UI and they can search on it if you need to reference it for any reason.

Some customers have a setting which automatically creates bills from Charges assuming the information needed is there.

Customers that use this functionality have an ‘Inbound Charges’ queue in their ‘Financials’ experience:

![](https://files.readme.io/896fd4e2e111abdfcd8fe6dc13a51fb22bb8a67a5d2b194111f4a856eff9d38f-image.png)

If they are Auto-creating bills from charges, you may want to instruct your customers to check the New Bills tab if they are looking for something they are expecting to be here.