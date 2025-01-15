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
Base Profile: <https://www.hl7.org/fhir/documentreference.html>

There are several different Document categories and types inside of EMA. Most “documents” can be handled through the ‘DocumentReference’ resource.

#### **Attachments**

Each Patient chart has a section called ‘Attachments’

![](https://files.readme.io/b1dba00eef180cd84ae6314cb675c33facf828f837649772cbdb91caa83b4540-image.png)

Each document has the ability to have a title, category, file name, visit associated (if relevant), and date. The document categories in this section are defined by the customer. Each customer will have different document categories and therefore different IDs for these categories. Each customer’s document categories can be found by querying their ValueSet.

#### **Visit Notes**

The Visit Note is another document type you can find in EMA. These are the nicely designed PDFs of each patient encounter in EMA. You can find ALL of a Patient’s visit notes, by calling: /DocumentReference?patient={patientID}&category=note.  
If you are looking for the Visit Note of a specific Encounter, you can /DocumentReference/note|{visitID}. You can find Encounters by searching the /Encounter endpoint.

#### **CCDA**

You can also query for a Patient’s CCDA. /DocumentReference?patient={patientID}&category=CCDA. This will be an XML document.

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

- Add Documents to a Patient’s chart
- Find Documents for a Patient
- Find a specific Visit Note
- Retrieve a Patient’s CCDA

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The MMI-specific unique identifier for the Document",
    "1-0": "identifier",
    "1-1": "filename",
    "2-0": "status",
    "2-1": "current | superseded | entered-in-error  \nNOTE: MMI currently only supports ‘current’",
    "3-0": "type",
    "3-1": "the type of file  \n  \n- application/pdf\n- audio/mpeg",
    "4-0": "category",
    "4-1": "ValueSet: document-category  \n{base url}/{firm_url_prefix}/ema/fhir/v2/ValueSet/document-category",
    "5-0": "subject",
    "5-1": "reference - Patient",
    "6-0": "date",
    "6-1": "When this document reference was created",
    "7-0": "description",
    "7-1": "The title of the document",
    "8-0": "content",
    "8-1": "The document itself",
    "9-0": "context",
    "9-1": "Reference to Encounter"
  },
  "cols": 2,
  "rows": 10,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The Following Operations are supported:

- DocumentReference READ
- DocumentReference SEARCH
- DocumentReference CREATE

**DocumentReference CCDA and Visit Notes**

Additionally, we’ve added functionality to be able to retrieve:

- A Patient’s CCDA Document (an XML document)
- A Patient’s Visit Note - the PDF version of a visit note for a specific encounter

<br />

#### CCDA

In order to search for a patient’s CCDA:

[block:parameters]
{
  "data": {
    "h-0": "HTTP Request",
    "h-1": "Method",
    "h-2": "Action",
    "0-0": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/DocumentReference?patient=(PatientID}&category=ccda",
    "0-1": "GET",
    "0-2": "Search for a Patient’s CCDA  \n  \nAlternatively, the LOINC for CCDA (81214-9) can be passed instead of ‘ccda’",
    "1-0": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/DocumentReference/ccda|{patientID}",
    "1-1": "GET",
    "1-2": "Retrieve a Patient’s CCDA  \n  \nAlternatively, the LOINC for CCDA (81214-9) can be passed instead of ‘ccda’"
  },
  "cols": 3,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


<br />

#### Visit Note

In order to search for a patient’s Visit Note(s):

[block:parameters]
{
  "data": {
    "h-0": "HTTP Request",
    "h-1": "Method",
    "h-2": "Action",
    "0-0": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/DocumentReference?patient={PatientID}&category=note",
    "0-1": "GET",
    "0-2": "Search for a Patient’s Visit Note  \n  \nAlternatively, the LOINC for Summary of episode note (34133-9) can be passed instead of ‘note’",
    "1-0": "{baseurl}/{firm_url_prefix}/ema/fhir/v2/DocumentReference/note|{visitID}",
    "1-1": "GET",
    "1-2": "Retrieve a Patient’s Visit Note  \n  \nAlternatively, the LOINC for Summary of episode note (34133-9) can be passed instead of ‘note’"
  },
  "cols": 3,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


***

<br />

### DocumentReference CREATE

[block:parameters]
{
  "data": {
    "h-0": "Step",
    "h-1": "HTTP Request",
    "h-2": "Method",
    "h-3": "Action",
    "0-0": "1",
    "0-1": "{base url}/{firm_url_prefix}/ema/fhir/v2/Binary",
    "0-2": "POST",
    "0-3": "Retrieve S3 Bucket URL",
    "1-0": "2",
    "1-1": "{base_s3_url}/{auto-generated string}  \n  \n**NOTE**:‘base_s3_url’ refers to the URL you will get back from making the Binary POST. There will be different URL structures depending on whether you are POSTing to Development or Production environments. As an example, here is an example of the current development URL:  \n  \n<https://modmed-prod-incoming-fhir-attachments.s3.amazonaws.com/{auto-generated_string}>",
    "1-2": "PUT",
    "1-3": "Upload the document to the S3 URL  \n  \n**Note**: If using Postman, or a similar solution, check your hidden headers as it may automatically add a Content-Type which may cause the upload to fail. Content-Type will need to equal “text/plain”",
    "2-0": "3",
    "2-1": "{base url}/{firm_url_prefix}/ema/fhir/v2/DocumentReference",
    "2-2": "POST",
    "2-3": "Upload document from S3 URL to EMA"
  },
  "cols": 4,
  "rows": 3,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


<br />

The attributes for creating a document are:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "identifier\\*",
    "0-1": "filename",
    "0-2": "The name of the file",
    "1-0": "content\\*",
    "1-1": "S3 URL returned via POST against the Binary resource in step 1",
    "1-2": "The actual contents of the document",
    "2-0": "subject",
    "2-1": "patient reference",
    "2-2": "Use this to associate the document to the correct patient. it is not required.  \n  \nAny document posted without a patient will go into an unassociated queue where someone at the practice will need to manually associate the document to a patient.",
    "3-0": "title",
    "3-1": "string",
    "3-2": "The title of the file - not required, but there is a title column in the UI. This could be used to give a little more information than what is in the name of the file.",
    "4-0": "creation",
    "4-1": "datetime",
    "4-2": "When passed in, this will set the ‘Original Creation Date’ in EMA so that  \nwhen a user is searching for attachments in a patient’s chart, the user will see this date as the date rather than the date the document was uploaded into EMA."
  },
  "cols": 3,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


**Step 1**: We’ve added the ‘Binary’ resource as a mechanism to retrieve an S3 URL for your customer’s site. You will need to create a POST to this Endpoint in order to retrieve the URL. The POST can simply be blank, however, here is a sample of a payload if you want to use something like this:

POST {base url}/{firm_url_prefix}/ema/fhir/v2/Binary

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