---
title: Documents
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
Base Profile: [https://www.hl7.org/fhir/documentreference.html](https://www.hl7.org/fhir/documentreference.html)

There are several different Document categories and types inside of EMA. Most “documents” can be handled through the ‘DocumentReference’ resource.

#### **Attachments**

Each Patient chart has a section called ‘Attachments’

![](https://files.readme.io/b1dba00eef180cd84ae6314cb675c33facf828f837649772cbdb91caa83b4540-image.png)

Each document has the ability to have a title, category, file name, visit associated (if relevant), and date. The document categories in this section are defined by the customer. Each customer will have different document categories and therefore different IDs for these categories. Each customer’s document categories can be found by querying their ValueSet.

#### **Visit Notes**

The Visit Note is another document type you can find in EMA. These are the nicely designed PDFs of each patient encounter in EMA. You can find ALL of a Patient’s visit notes, by calling: /DocumentReference?patient=\{patientID}\&category=note.\
If you are looking for the Visit Note of a specific Encounter, you can /DocumentReference/note|\{visitID}. You can find Encounters by searching the /Encounter endpoint.

#### **CCDA**

You can also query for a Patient’s CCDA. /DocumentReference?patient=\{patientID}\&category=CCDA. This will be an XML document.

#### **Results**

In order to POST a document into a customer’s Results Log, you would need to query their ValueSet for document-category and find the ‘Results -\*’ categories. Each customer will have Results categories - depending on the type of results they work with - for example:

```Text json
{
  "code": "1567",
  "display": "Results - Lab"
},
{
  "code": "31755",
  "display": "Results - Path/Lab"
},
{
  "code": "1694",
  "display": "Results - Pathology"
},
{
  "code": "2075",
  "display": "Results - Procedures"
},
{
  "code": "5184",
  "display": "Results - PT/OT"
},
{
  "code": "1821",
  "display": "Results - Radiology"
},

```

The end experience will be an entry into the customer’s Results Log:

![](https://files.readme.io/8117e389002a683266e949bce46a4f5b116a02bcee4ef8699b91ec62548fad71-image.png)

The results log allows for a more Results-centric workflow which allows the end user to review, sign, and/or create plans or follow-up actions.

***

## DocumentReference

The **DocumentReference** resource can be used to retrieve or create documents located in the "Attachments" section of a patient's chart in EMA. This documentation specifically pertains to the "Attachments" section.

For details on how to retrieve a patient's **CCDA** or **Visit Note**, please refer to the **DocumentReference CCDA** and **Visit Notes** documentation in the following section.

If you're looking to POST a **Patient Reported Outcome (PRO)** document to EMA’s PRO module, please consult the **PRO** portion of the **DocumentReference CREATE** section below.

Common use cases include:

* Add Documents to a Patient’s chart
* Find Documents for a Patient
* Find a specific Visit Note
* Retrieve a Patient’s CCDA

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
        The MMI-specific unique identifier for the Document
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        filename
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        status
      </td>

      <td style={{ textAlign: "left" }}>
        current | superseded | entered-in-error\
        NOTE: MMI currently only supports ‘current’
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        the type of file  

        * application/pdf
        * audio/mpeg
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        category
      </td>

      <td style={{ textAlign: "left" }}>
        ValueSet: document-category\
        \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/document-category
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        reference - Patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        date
      </td>

      <td style={{ textAlign: "left" }}>
        When this document reference was created
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        description
      </td>

      <td style={{ textAlign: "left" }}>
        The title of the document
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        content
      </td>

      <td style={{ textAlign: "left" }}>
        The document itself
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        context
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Encounter
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* DocumentReference READ
* DocumentReference SEARCH
* DocumentReference CREATE

**DocumentReference CCDA and Visit Notes**

Additionally, we’ve added functionality to be able to retrieve:

* A Patient’s CCDA Document (an XML document)
* A Patient’s Visit Note - the PDF version of a visit note for a specific encounter

<br />

#### CCDA

In order to search for a patient’s CCDA:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
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
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/DocumentReference?patient=(PatientID}\&category=ccda
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Search for a Patient’s CCDA  

        Alternatively, the LOINC for CCDA (81214-9) can be passed instead of ‘ccda’
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/DocumentReference/ccda|\{patientID}
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Retrieve a Patient’s CCDA  

        Alternatively, the LOINC for CCDA (81214-9) can be passed instead of ‘ccda’
      </td>
    </tr>
  </tbody>
</Table>

<br />

#### Visit Note

In order to search for a patient’s Visit Note(s):

<Table align={["left","left","left"]}>
  <thead>
    <tr>
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
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/DocumentReference?patient=\{PatientID}\&category=note
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Search for a Patient’s Visit Note  

        Alternatively, the LOINC for Summary of episode note (34133-9) can be passed instead of ‘note’
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/DocumentReference/note|\{visitID}
      </td>

      <td style={{ textAlign: "left" }}>
        GET
      </td>

      <td style={{ textAlign: "left" }}>
        Retrieve a Patient’s Visit Note  

        Alternatively, the LOINC for Summary of episode note (34133-9) can be passed instead of ‘note’
      </td>
    </tr>
  </tbody>
</Table>

***

<br />

### DocumentReference CREATE

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
        \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Binary
      </td>

      <td style={{ textAlign: "left" }}>
        POST
      </td>

      <td style={{ textAlign: "left" }}>
        Retrieve S3 Bucket URL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        2
      </td>

      <td style={{ textAlign: "left" }}>
        \{base\_s3\_url}/\{auto-generated string}  

        * \*NOTE\*\*:‘base\_s3\_url’ refers to the URL you will get back from making the Binary POST. There will be different URL structures depending on whether you are POSTing to Development or Production environments. As an example, here is an example of the current development URL:  

        [https://modmed-prod-incoming-fhir-attachments.s3.amazonaws.com/\{auto-generated\_string}](https://modmed-prod-incoming-fhir-attachments.s3.amazonaws.com/\{auto-generated_string})
      </td>

      <td style={{ textAlign: "left" }}>
        PUT
      </td>

      <td style={{ textAlign: "left" }}>
        Upload the document to the S3 URL  

        * \*Note\*\*: If using Postman, or a similar solution, check your hidden headers as it may automatically add a Content-Type which may cause the upload to fail. Content-Type will need to equal “text/plain”
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        3
      </td>

      <td style={{ textAlign: "left" }}>
        \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/DocumentReference
      </td>

      <td style={{ textAlign: "left" }}>
        POST
      </td>

      <td style={{ textAlign: "left" }}>
        Upload document from S3 URL to EMA
      </td>
    </tr>
  </tbody>
</Table>

<br />

The attributes for creating a document are:

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
        identifier\*
      </td>

      <td style={{ textAlign: "left" }}>
        filename
      </td>

      <td style={{ textAlign: "left" }}>
        The name of the file
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        content\*
      </td>

      <td style={{ textAlign: "left" }}>
        S3 URL returned via POST against the Binary resource in step 1
      </td>

      <td style={{ textAlign: "left" }}>
        The actual contents of the document
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subject
      </td>

      <td style={{ textAlign: "left" }}>
        patient reference
      </td>

      <td style={{ textAlign: "left" }}>
        Use this to associate the document to the correct patient. it is not required.  

        Any document posted without a patient will go into an unassociated queue where someone at the practice will need to manually associate the document to a patient.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        title
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The title of the file - not required, but there is a title column in the UI. This could be used to give a little more information than what is in the name of the file.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        creation
      </td>

      <td style={{ textAlign: "left" }}>
        datetime
      </td>

      <td style={{ textAlign: "left" }}>
        When passed in, this will set the ‘Original Creation Date’ in EMA so that\
        when a user is searching for attachments in a patient’s chart, the user will see this date as the date rather than the date the document was uploaded into EMA.
      </td>
    </tr>
  </tbody>
</Table>

**Step 1**: We’ve added the ‘Binary’ resource as a mechanism to retrieve an S3 URL for your customer’s site. You will need to create a POST to this Endpoint in order to retrieve the URL. The POST can simply be blank, however, here is a sample of a payload if you want to use something like this:

POST \{base url}/\{firm\_url\_prefix}/ema/fhir/v2/Binary

```Text json
{
  "resourceType" : "Binary",
  "contentType" : "application/pdf",
  "securityContext" : null,
  "data" : null
}
```

Note: The generated S3 URL will expire after 5 minutes. You will then need to POST the Binary Resource for a new S3 URL

**Step 2**: PUT Document to S3 URL. This will require you to place the document into the S3 bucket. This can be done a variety of ways - one example:

```Text http
curl --location --request PUT '{base_s3_url}/{auto-generated string}' \
--header 'Content-Type: text/plain' \
--data-binary '@/Users/folder/Downloads/test.pdf'
```

Note: If using Postman, or a similar solution, check your hidden headers as it may automatically add a Content-Type which may cause the upload to fail. Content-Type will need to equal “text/plain”

**Step 3**: POST New Document with Patient ID

```Text json
{
  "fullUrl": "{base url}/{firm_url_prefix}/ema/fhir/v2/DocumentReference?patient=7132",
  "resourceType": "DocumentReference",
  "identifier": [
    {
      "system": "filename",
      "value": "mikes-file.pdf"
    }
  ],
  "status": "current",
  "type": {
    "text": "application/pdf"
  },
  "category": [
    {
      "coding": [
        {
          "system": "{base url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/document-category",
          "code": "426",
          "display": "External Visit Note"
        }
      ],
      "text": "External Visit Note"
    }
  ],
  "subject": {
    "reference": "{base url}/{firm_url_prefix}/Patient/7132",
    "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/7132"
  },
  "date": "2019-04-03T21:11:38.000+00:00",
  "content": [
    {
      "attachment": {
        "title": "Mike's PDF",
        "contentType": "application/pdf",
        "url": "{base_s3_url}/{auto-generated string}/{auto-generated string}",
        "size": 383176,
        "creation": "2019-04-03T21:11:38+00:00"
      }
    }
  ]
}
```

***

<br />

### Patient Reported Outcomes (PROS)

In addition to being able to create attachments in the patient’s chart, we’ve also enabled the ability to post documents into the EMA PRO module. In order to do this, you must send the category as defined in the payload below:

```Text json
{
  "resourceType": "DocumentReference",
  "identifier": [
    {
      "system": "filename",
      "value": "PRO-sample.pdf"
    }
  ],
  "status": "current",
  "type": {
    "text": "application/pdf"
  },
  "category": [
    {
      "coding": [
        {
          "system": "{base url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/document-type",
          "code": "PROS",
          "display": "Patient Reported Outcomes"
        }
      ],
      "text": "Patient Reported Outcomes"
    }
  ],
  "subject": {
    "reference": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/6353",
    "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Patient/6353"
  },
  "date": "2021-03-10T18:04:09+00:00",
  "description": "PRO-sample",
  "content": [
    {
      "attachment": {
        "url": "{base_s3_url}/{auto-generated string}/{auto-generated string}",
        "size": 26654,
        "title": "PRO-sample",
        "creation": "2021-03-10T18:04:09+00:00"
      }
    }
  ],
  "context": {
    "encounter": [
      {
        "reference": "{base url}/{firm_url_prefix}/ema/fhir/v2/Encounter/266237",
        "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Encounter/266237"
      }
    ],
    "related": [
      {
        "reference": "{base url}/{firm_url_prefix}/ema/fhir/v2/Practitioner/1178",
        "display": "{base url}/{firm_url_prefix}/ema/fhir/v2/Practitioner/1178"
      }
    ]
  }
}
```
