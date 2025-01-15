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
Base Profile: [https://www.hl7.org/fhir/coverage.html](https://www.hl7.org/fhir/coverage.html)

The insurance experience will differ if the customer uses MMPM (ModMed Practice Management) or if they are only using EMA. You will not be able to CREATE or UPDATE a patient’s insurance if the customer is not using MMPM.

Common use cases include:

* Find Insurance Coverage for a patient
* Find the Primary, Secondary, Tertiary coverages for a Patient

**Note:** There are currently two versions of the Coverage READ and Coverage SEARCH payloads. We recently added the ability to do a Coverage CREATE and when we did that, we changed the structure of the Coverage payload. Because we didn’t want to introduce a breaking change to the vendors who were already using the Coverage endpoint, we put the new version of the Coverage payload behind a feature flag. If you need this updated version, please contact [synapsys@modmed.com](mailto:synapsys@modmed.com) in order to turn the flag on for your customers. At some point, we will communicate the change to the entire audience and vendors will have to use the updated version.

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
        The MMI-specific unique identifier for the coverage
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        payerId
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet/insurance-policy-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        policyHolder
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        beneficiary
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        relationship
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet/insured-relationship
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        payor
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        class
      </td>

      <td style={{ textAlign: "left" }}>
        [https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-plan](https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-plan)\
        [https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-group](https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-group)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        order
      </td>

      <td style={{ textAlign: "left" }}>
        1=Primary\
        2=Secondary\
        3=Tertiary\
        0=Non-ordered\
        Please note that any insurance that is not Primary, Secondary, Tertiary will return as order=0
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        costToBeneficiary
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* Coverage READ
* Coverage SEARCH
* Coverage CREATE
* Coverage UPDATE

### Coverage CREATE

The ModMed Practice Management (MMPM) system allows external systems to create new **Coverages** for patients. Once a new coverage is submitted, it will be reviewed and reconciled by someone at the practice.

**Key Points:**

* **Payer Support:**\
  When submitting a new coverage, ensure that it is for a **Payer** supported by the PM system. Some practices may also require that you create coverage for a specific **InsurancePlan** that is supported by the system.
* **ID Card Submission:**\
  You have the option to include images of the insurance ID card (front and back), although this is not mandatory.
* **Reconciliation Process:**\
  Since coverage submissions require manual reconciliation by the practice, when you POST a new coverage, the system will return a **ReconciliationID**. This ID allows you to query the status of the coverage while it is pending.
* **Status Check:**\
  You can use the API to check if the coverage is still pending or if it has been reconciled. Once reconciliation is complete, you will need to query the patient's **Coverages** to get the current information.

The following steps outline how you can query the system to identify and track these coverages.

**User Experience:**\
A vendor has the ability to capture and send all of the following data:

* Payer Name
* Plan
* Policy Type
* Policy Number
* Group Number
* Patient's Name on Insurance Card
* Co-Pay Amount
* Co-Insurance %
* Deductible
* Patient's Relationship to Policy Holder
* Name (Policy Holder)
* Date of Birth (Policy Holder)
* Birth Sex (Policy Holder)
* Address 1 (Policy Holder)
* Address 2 (Policy Holder)
* City (Policy Holder)
* State (Policy Holder)
* Zip (Policy Holder)
* Home Phone Number (Policy Holder)
* Work Phone Number (Policy Holder)
* Mobile Phone Number (Policy Holder)
* Remaining Deductible
* Out of Pocket
* Remaining Out of Pocket
* Policy Effective Date
* Policy End Date
* Insurance Card Image (Front of Card)
* Insurance Card Image (Back of Card)

Assuming all (or some) of that is included, the EMA/MMPM user would see this when they went to the Patient’s chart:

![](https://files.readme.io/6a1c2b8452ea9b4444a89889682212699a4d9c391c64730b33056bd85b43a230-image.png)

Essentially from there, the user can Accept All or reject All or go through and accept and reject different fields if they so choose. If the user accepts the insurance, it will become the Primary Insurance by default and the user will need to go to the ‘Insurance’ section of the Patient’s chart to change the order. If the user rejects the insurance, the vendor would need to send another message to get different insurance information there. If the user takes no action, a prompt will remain in the patient’s chart from which the user can return and choose to take action at any time.

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Step
      </th>

      <th style={{ textAlign: "left" }}>
        HTTP Request
      </th>

      <th style={{ textAlign: "left" }}>
        Method
      </th>

      <th style={{ textAlign: "left" }}>
        Action
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        1
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/Patient?\{Parameter=Value}
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Perform a Patient SEARCH to retrieve the Patient Id    

        Reference Patient SEARCH for a list of parameters
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        2
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/Coverage?\{patient=xxxxx}
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Find a patient’s existing Coverage(s)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        3
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/Organization?type=pay
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Perform an Organization SEARCH to retrieve the ID.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        4
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/InsurancePlan?owned-by=\{organization ID}
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        OPTIONAL (if the practice requires a supported InsurancePlan)    

        Perform an InsurancePlan SEARCH to retrieve the InsurancePlan Id , and the\
        insurance-policy-type    

        Reference InsurancePlan SEARCH for a list of parameters
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        5
      </td>

      <td style={{ textAlign: "left" }}>
        \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Binary
      </td>

      <td style={{ textAlign: "left" }}>
        POST
      </td>

      <td style={{ textAlign: "left" }}>
        OPTIONAL    

        Used to add the ID card images. This step will retrieve the S3 Bucket URL. One S3 URL will need to be generated for each image (front/back)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        6
      </td>

      <td style={{ textAlign: "left" }}>
        \{base\_s3\_url}/\{auto-generated string}
      </td>

      <td style={{ textAlign: "left" }}>
        PUT
      </td>

      <td style={{ textAlign: "left" }}>
        OPTIONAL    

        Upload insurance card images to the S3 Bucket URLs. One S3 Bucket URL will need to be used for each image (front/back)    

        NOTE: ‘base\_s3\_url’ refers to the URL you will get back from making the Binary POST. There will be different URL structures depending on whether you are POSTing to Development or Production environments. As an example, here is an example of the current Production URL:   

        https\://modmed-prod-incoming-fhir-at\
        tachments.s3.amazonaws.com/\{auto-g\
        enerated string}    

        Note: If using Postman, or a similar solution, check your hidden headers as it may automatically add a Content-Type which may cause the upload to fail. Content-Type will need to equal “text/plain”
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        7
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/insured-relationship
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        OPTIONAL   

        If relationship ≠ SELF, perform a GET on ValueSet insured-relationship to retrieve the relationship type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        8
      </td>

      <td style={{ textAlign: "left" }}>
        \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Coverage
      </td>

      <td style={{ textAlign: "left" }}>
        POST
      </td>

      <td style={{ textAlign: "left" }}>
        Use information gathered in 1-7 when constructing the Coverage payload
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        9
      </td>

      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/Coverage?reconciliationId=\{Reconciliation Id}
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Perform a Coverage SEARCH by the Reconciliation Identifier provided in the response to step 8 (if successful) to see if the Reconciliation is Pending or Completed
      </td>
    </tr>
  </tbody>
</Table>

The minimum attributes for creating a new Coverage are:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Name
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        only “active” supported on create
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        policyHolder information is only required when relationship is ≠ SELF   

        PolicyHolderFirst\
        PolicyHolderLast\
        PolicyHolderMiddle\
        PolicyHolderSuffix\
        PolicyHolderDOB\
        PolicyHolderBirthSex\
        PolicyHolderAddress1\
        PolicyHolderAddress2\
        PolicyHolderAddressCity\
        PolicyHolderAddressState\
        PolicyHolderAddressZipCode\
        PolicyHolderPhoneHome\
        PolicyHolderPhoneMobile\
        PolicyHolderPhoneWork\
        InsuranceCardFrontUrl (always optional)\
        InsuranceCardBackUrl (always optional)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        payor
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Organization Id
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        beneficiary
      </td>

      <td style={{ textAlign: "left" }}>
        reference
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Patient Id
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Policy Type ValueSet\
        \{baseurl}/\{firm\_url\_prefix}/ValueSet/insurance-policy-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        relationship
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Insured Relationship ValueSet   

        \{baseurl}/\{firm\_url\_prefix}/ValueSet/insured-relationship   

        NOTE: If relationship ≠ SELF, use the “identifier” attribute to pass the patients identifiers
      </td>
    </tr>
  </tbody>
</Table>

Additional attributes for creating a new Coverage are:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Name
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        order
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The order of the insurance policy, it can be 1= Primary , 2= Secondary 3 = Tertiary
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        class
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        Use this to pass in the Plan and/or Group Numbers and Names.  

        For Plans, use the Reference to Coverage Class Plan   

        [https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-plan](https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-plan)    

        For Groups, use the Reference to Coverage Class Group:    

        [https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-group](https://www.hl7.org/fhir/codesystem-coverage-class.html#coverage-class-group)    

        And then add values and names per the examples below.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        cost-to-beneficiary-type
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Cost to Beneficiary ValueSet    

        \{baseurl}/\{firm\_url\_prefix}/ValueSet/cost-to-beneficiary-type
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        period
      </td>

      <td style={{ textAlign: "left" }}>
        date
      </td>

      <td style={{ textAlign: "left" }}>
        Policy Effective Date and Policy End Date   

        start = yyyy-MM-dd\
        end = yyyy-MM-dd
      </td>
    </tr>
  </tbody>
</Table>

**Note:** Every inbound Coverage will need to be reconciled by the Firm. Searching Coverage by reconciliationId allows you to check the status of Reconciliation for the new Coverage. When the status of a reconciliationId is completed, the new Coverage has either been accepted or rejected. You can perform a Coverage READ or SEARCH to check to see if the Coverage was accepted.\
Perform a Coverage SEARCH by the Reconciliation Identifier provided in the response to step 8 (if successful) to see if the Reconciliation is Pending or Completed.

### Coverage UPDATE

Everything that can be added via a POST or CREATE can also be updated through a PUT. In that case, simply include the ID of the Coverage that you are updating.
