---
title: Patient
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient](http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient)

The Patient endpoint in FHIR is used to manage patient information. Here is a general description and a sample response of the FHIR Patient endpoint, highlighting its key components:

## Key Components of the FHIR Patient Resource

1. **id**: A unique identifier for the patient.
2. **identifier**: An array of identifiers for the patient (e.g., MRN, SSN).
3. **active**: Indicates if the patient's record is active.
4. **name**: An array of names for the patient.
5. **telecom**: Contact details for the patient, such as phone number or email.
6. **gender**: The gender of the patient (e.g., male, female, other).
7. **birthDate**: The date of birth of the patient.
8. **address**: Addresses related to the patient.
9. **contact**: Contact persons for the patient.
10. **managingOrganization**: The organization responsible for the patient.
11. **link**: References to other patient resources linked to this patient.

**Sample Response Object:**

```Text json
{
 "resourceType": "Patient",
 "id": "example",
 "text": {
   "status": "generated",
   "div": "<div><p>John Doe</p></div>"
 },
 "identifier": [
   {
     "use": "usual",
     "type": {
       "coding": [
         {
           "system": "http://hl7.org/fhir/v2/0203",
           "code": "MR",
           "display": "Medical record number"
         }
       ],
       "text": "MRN"
     },
     "system": "http://hospital.smarthealthit.org",
     "value": "12345"
   }
 ],
 "active": true,
 "name": [
   {
     "use": "official",
     "family": "Doe",
     "given": [
       "John"
     ]
   },
   {
     "use": "nickname",
     "given": [
       "Johnny"
     ]
   }
 ],
 "telecom": [
   {
     "system": "phone",
     "value": "555-555-5555",
     "use": "home"
   },
   {
     "system": "email",
     "value": "john.doe@example.com",
     "use": "work"
   }
 ],
 "gender": "male",
 "birthDate": "1974-12-25",
 "address": [
   {
     "use": "home",
     "type": "both",
     "line": [
       "123 Main St"
     ],
     "city": "Somewhere",
     "state": "CA",
     "postalCode": "90210",
     "country": "USA"
   }
 ],
 "contact": [
   {
     "relationship": [
       {
         "coding": [
           {
             "system": "http://hl7.org/fhir/v2/0131",
             "code": "N",
             "display": "Next of Kin"
           }
         ],
         "text": "Next of Kin"
       }
     ],
     "name": {
       "family": "Doe",
       "given": [
         "Jane"
       ]
     },
     "telecom": [
       {
         "system": "phone",
         "value": "555-555-1234",
         "use": "home"
       }
     ],
     "address": {
       "line": [
         "123 Main St"
       ],
       "city": "Somewhere",
       "state":
"CA",
       "postalCode": "90210",
       "country": "USA"
     },
     "gender": "female"
   }
 ],
 "managingOrganization": {
   "reference": "Organization/1",
   "display": "Example Organization"
 }
}
```

***

## Export

The GET: /Patient/$export endpoint is part of the FHIR Bulk Data Access specification, which allows large-scale export of data from a FHIR server. This endpoint supports exporting data in bulk for a set of patients, letting clients efficiently fetch large amounts of data for further processing or analysis. Here’s a general description:

<br />

### Key Concepts

1. **Asynchronous Request**: The export operation is typically performed asynchronously. The server acknowledges the request and processes it in the background. Clients must periodically poll the server to check the status of the export.
2. **Bulk Data Export**: The response contains links to files that can be downloaded. These files include data related to patients, such as demographic information, medical histories, and other clinical data.
3. **NDJSON Format**: Data is generally exported in Newline Delimited JSON (NDJSON) format for efficient parsing and processing.

<br />

### Request

`GET [base]/Patient/$export`

<br />

### Query Parameters

* **\_outputFormat** (optional): Specifies the format of the generated files (e.g., application/fhir+ndjson).
* **\_since** (optional): Only include resource versions updated after this time.
* **\_type** (optional): Specifies the types of resources to be included in the export.
* **\_typeFilter** (optional): A parameter to filter the resources further.

<br />

### Example Request

```Text http
GET /Patient/$export?\_outputFormat=application/fhir+ndjson&\_since=2021-01-01T00:00:00Z&\_type=Patient,Observation
```

<br />

### Initial Response

An initial response confirms that the export request has been received and provides a URL to check the status of the request.

```Text http
202 Accepted  
Content-Location: [status_endpoint_URL]
```

<br />

### Status Check

Clients can poll the Content-Location URL to check the status of their request. If the export is still processing, the server responds with status information.

```Text http
GET [status_endpoint_URL]
```

<br />

### Completed Response

When the export is complete, the status check URL provides the files for download.

```Text http
200 OK  
{  
  "transactionTime": "2023-10-01T00:00:00Z",  
  "request": "/Patient/$export?\_outputFormat=application/fhir+ndjson&\_type=Patient,Observation",  
  "requiresAccessToken": true,  
  "output": \[  
    {  
      "type": "Patient",  
      "url": "[download_URL_for_Patient_data]"  
    },  
    {  
      "type": "Observation",  
      "url": "[download_URL_for_Observation_data]"  
    }  
  ]  
}
```

<br />

### Error Handling

If there are any errors during the export process, the status check response will include details about the issues encountered.
