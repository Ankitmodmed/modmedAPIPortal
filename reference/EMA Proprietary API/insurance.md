---
title: Insurance
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
Base Profile: <https://www.hl7.org/fhir/coverage.html>

The insurance experience will differ if the customer uses MMPM (ModMed Practice Management) or if they are only using EMA. You will not be able to CREATE or UPDATE a patient’s insurance if the customer is not using MMPM.

Common use cases include:

- Find Insurance Coverage for a patient
- Find the Primary, Secondary, Tertiary coverages for a Patient

**Note:** There are currently two versions of the Coverage READ and Coverage SEARCH payloads. We recently added the ability to do a Coverage CREATE and when we did that, we changed the structure of the Coverage payload. Because we didn’t want to introduce a breaking change to the vendors who were already using the Coverage endpoint, we put the new version of the Coverage payload behind a feature flag. If you need this updated version, please contact [synapsys@modmed.com](mailto:synapsys@modmed.com) in order to turn the flag on for your customers. At some point, we will communicate the change to the entire audience and vendors will have to use the updated version.

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The MMI-specific unique identifier for the coverage",
    "1-0": "identifier",
    "1-1": "payerId",
    "2-0": "status",
    "2-1": "",
    "3-0": "type",
    "3-1": "ValueSet/insurance-policy-type",
    "4-0": "policyHolder",
    "4-1": "",
    "5-0": "beneficiary",
    "5-1": "reference",
    "6-0": "relationship",
    "6-1": "ValueSet/insured-relationship",
    "7-0": "payor",
    "7-1": "",
    "8-0": "class",
    "8-1": "<https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-plan>  \n<https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-group>",
    "9-0": "order",
    "9-1": "1=Primary  \n2=Secondary  \n3=Tertiary  \n0=Non-ordered  \nPlease note that any insurance that is not Primary, Secondary, Tertiary will return as order=0",
    "10-0": "costToBeneficiary",
    "10-1": ""
  },
  "cols": 2,
  "rows": 11,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- Coverage READ
- Coverage SEARCH
- Coverage CREATE
- Coverage UPDATE

### Coverage CREATE

The ModMed Practice Management (MMPM) system allows external systems to create new **Coverages** for patients. Once a new coverage is submitted, it will be reviewed and reconciled by someone at the practice.

**Key Points:**

- **Payer Support:**  
  When submitting a new coverage, ensure that it is for a **Payer** supported by the PM system. Some practices may also require that you create coverage for a specific **InsurancePlan** that is supported by the system.
- **ID Card Submission:**  
  You have the option to include images of the insurance ID card (front and back), although this is not mandatory.
- **Reconciliation Process:**  
  Since coverage submissions require manual reconciliation by the practice, when you POST a new coverage, the system will return a **ReconciliationID**. This ID allows you to query the status of the coverage while it is pending.
- **Status Check:**  
  You can use the API to check if the coverage is still pending or if it has been reconciled. Once reconciliation is complete, you will need to query the patient's **Coverages** to get the current information.

The following steps outline how you can query the system to identify and track these coverages.

**User Experience:**  
A vendor has the ability to capture and send all of the following data:

- Payer Name
- Plan
- Policy Type
- Policy Number
- Group Number
- Patient's Name on Insurance Card
- Co-Pay Amount
- Co-Insurance %
- Deductible
- Patient's Relationship to Policy Holder
- Name (Policy Holder)
- Date of Birth (Policy Holder)
- Birth Sex (Policy Holder)
- Address 1 (Policy Holder)
- Address 2 (Policy Holder)
- City (Policy Holder)
- State (Policy Holder)
- Zip (Policy Holder)
- Home Phone Number (Policy Holder)
- Work Phone Number (Policy Holder)
- Mobile Phone Number (Policy Holder)
- Remaining Deductible
- Out of Pocket
- Remaining Out of Pocket
- Policy Effective Date
- Policy End Date
- Insurance Card Image (Front of Card)
- Insurance Card Image (Back of Card)

Assuming all (or some) of that is included, the EMA/MMPM user would see this when they went to the Patient’s chart:

![](https://files.readme.io/6a1c2b8452ea9b4444a89889682212699a4d9c391c64730b33056bd85b43a230-image.png)

Essentially from there, the user can Accept All or reject All or go through and accept and reject different fields if they so choose. If the user accepts the insurance, it will become the Primary Insurance by default and the user will need to go to the ‘Insurance’ section of the Patient’s chart to change the order. If the user rejects the insurance, the vendor would need to send another message to get different insurance information there. If the user takes no action, a prompt will remain in the patient’s chart from which the user can return and choose to take action at any time.

[block:parameters]
{
  "data": {
    "h-0": "Step",
    "h-1": "HTTP Request",
    "h-2": "Method",
    "h-3": "Action",
    "0-0": "1",
    "0-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/Patient?{Parameter=Value}",
    "0-2": "GET",
    "0-3": "Perform a Patient SEARCH to retrieve the Patient Id    \n  \nReference Patient SEARCH for a list of parameters",
    "1-0": "2",
    "1-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/Coverage?{patient=xxxxx}",
    "1-2": "GET",
    "1-3": "Find a patient’s existing Coverage(s)",
    "2-0": "3",
    "2-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/Organization?type=pay",
    "2-2": "GET",
    "2-3": "Perform an Organization SEARCH to retrieve the ID.",
    "3-0": "4",
    "3-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/InsurancePlan?owned-by={organization ID}",
    "3-2": "GET",
    "3-3": "OPTIONAL (if the practice requires a supported InsurancePlan)    \n  \nPerform an InsurancePlan SEARCH to retrieve the InsurancePlan Id , and the  \ninsurance-policy-type    \n  \nReference InsurancePlan SEARCH for a list of parameters",
    "4-0": "5",
    "4-1": "{base url}/{firm_url_prefix}/ema/fhir/v2/Binary",
    "4-2": "POST",
    "4-3": "OPTIONAL    \n  \nUsed to add the ID card images. This step will retrieve the S3 Bucket URL. One S3 URL will need to be generated for each image (front/back)",
    "5-0": "6",
    "5-1": "{base_s3_url}/{auto-generated string}",
    "5-2": "PUT",
    "5-3": "OPTIONAL    \n  \nUpload insurance card images to the S3 Bucket URLs. One S3 Bucket URL will need to be used for each image (front/back)    \n  \nNOTE: ‘base_s3_url’ refers to the URL you will get back from making the Binary POST. There will be different URL structures depending on whether you are POSTing to Development or Production environments. As an example, here is an example of the current Production URL:   \n  \nhttps\\://modmed-prod-incoming-fhir-at  \ntachments.s3.amazonaws.com/{auto-g  \nenerated string}    \n  \nNote: If using Postman, or a similar solution, check your hidden headers as it may automatically add a Content-Type which may cause the upload to fail. Content-Type will need to equal “text/plain”",
    "6-0": "7",
    "6-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/insured-relationship",
    "6-2": "GET",
    "6-3": "OPTIONAL   \n  \nIf relationship ≠ SELF, perform a GET on ValueSet insured-relationship to retrieve the relationship type",
    "7-0": "8",
    "7-1": "{base url}/{firm_url_prefix}/ema/fhir/v2/Coverage",
    "7-2": "POST",
    "7-3": "Use information gathered in 1-7 when constructing the Coverage payload",
    "8-0": "9",
    "8-1": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/Coverage?reconciliationId={Reconciliation Id}",
    "8-2": "GET",
    "8-3": "Perform a Coverage SEARCH by the Reconciliation Identifier provided in the response to step 8 (if successful) to see if the Reconciliation is Pending or Completed"
  },
  "cols": 4,
  "rows": 9,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


The minimum attributes for creating a new Coverage are:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "status",
    "0-1": "code",
    "0-2": "only “active” supported on create",
    "1-0": "identifier",
    "1-1": "string",
    "1-2": "policyHolder information is only required when relationship is ≠ SELF   \n  \nPolicyHolderFirst  \nPolicyHolderLast  \nPolicyHolderMiddle  \nPolicyHolderSuffix  \nPolicyHolderDOB  \nPolicyHolderBirthSex  \nPolicyHolderAddress1  \nPolicyHolderAddress2  \nPolicyHolderAddressCity  \nPolicyHolderAddressState  \nPolicyHolderAddressZipCode  \nPolicyHolderPhoneHome  \nPolicyHolderPhoneMobile  \nPolicyHolderPhoneWork  \nInsuranceCardFrontUrl (always optional)  \nInsuranceCardBackUrl (always optional)",
    "2-0": "payor",
    "2-1": "reference",
    "2-2": "Reference to Organization Id",
    "3-0": "beneficiary",
    "3-1": "reference",
    "3-2": "Reference to Patient Id",
    "4-0": "type",
    "4-1": "code",
    "4-2": "Reference to Policy Type ValueSet  \n{baseurl}/{firm_url_prefix}/ValueSet/insurance-policy-type",
    "5-0": "relationship",
    "5-1": "code",
    "5-2": "Reference to Insured Relationship ValueSet   \n  \n{baseurl}/{firm_url_prefix}/ValueSet/insured-relationship   \n  \nNOTE: If relationship ≠ SELF, use the “identifier” attribute to pass the patients identifiers"
  },
  "cols": 3,
  "rows": 6,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


Additional attributes for creating a new Coverage are:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "order",
    "0-1": "string",
    "0-2": "The order of the insurance policy, it can be 1= Primary , 2= Secondary 3 = Tertiary",
    "1-0": "class",
    "1-1": "code",
    "1-2": "Use this to pass in the Plan and/or Group Numbers and Names.  \n  \nFor Plans, use the Reference to Coverage Class Plan   \n  \n<https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-plan>    \n  \nFor Groups, use the Reference to Coverage Class Group:    \n  \n<https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-group>    \n  \nAnd then add values and names per the examples below.",
    "2-0": "cost-to-beneficiary-type",
    "2-1": "ValueSet",
    "2-2": "Reference to Cost to Beneficiary ValueSet    \n  \n{baseurl}/{firm_url_prefix}/ValueSet/cost-to-beneficiary-type",
    "3-0": "period",
    "3-1": "date",
    "3-2": "Policy Effective Date and Policy End Date   \n  \nstart = yyyy-MM-dd  \nend = yyyy-MM-dd"
  },
  "cols": 3,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


**Note:** Every inbound Coverage will need to be reconciled by the Firm. Searching Coverage by reconciliationId allows you to check the status of Reconciliation for the new Coverage. When the status of a reconciliationId is completed, the new Coverage has either been accepted or rejected. You can perform a Coverage READ or SEARCH to check to see if the Coverage was accepted.  
Perform a Coverage SEARCH by the Reconciliation Identifier provided in the response to step 8 (if successful) to see if the Reconciliation is Pending or Completed.

### Coverage UPDATE

Everything that can be added via a POST or CREATE can also be updated through a PUT. In that case, simply include the ID of the Coverage that you are updating.