---
title: Group
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
Base Profile: [http://hl7.org/fhir/group.html](http://hl7.org/fhir/group.html)

The FHIR (Fast Healthcare Interoperability Resources) Group endpoint is part of the FHIR standard, which defines how healthcare information can be exchanged electronically. The Group resource represents a defined collection of entities that may be managed and acted upon as a whole. These entities can be patients, practitioners, devices, medications, etc.

### Key Components of a FHIR Group Resource

1. **id**: Unique identifier for the Group resource.
2. **identifier**: A distinct identification code for the Group.
3. **type**: The type of resource that the Group contains (e.g., person, animal, practitioner, device).
4. **actual**: Indicates whether the group is an actual group or a potential group (boolean).
5. **code**: The meaning of the group as a whole.
6. **name**: A label assigned to the group for human identification.
7. **quantity**: The number of members in the group.
8. **member**: The members that are part of the group. Each member includes an entity reference and a period indicating when the member was active in the group.

<br />

#### **Sample Response Object**

```Text json
{  
  "resourceType": "Group",  
  "id": "example",  
  "identifier": [  
    {  
      "system": "http://example.org/fhir/ids",  
      "value": "example-group"  
    }  
  ],  
  "type": "person",  
  "actual": true,  
  "code": {  
    "text": "VIP Patients"  
  },  
  "name": "VIP Patient Group",  
  "quantity": 5,  
  "member": [  
    {  
      "entity": {  
        "reference": "Patient/1"  
      },  
      "period": {  
        "start": "2020-01-01",  
        "end": "2020-12-31"  
      }  
    },  
    {  
      "entity": {  
        "reference": "Patient/2"  
      },  
      "period": {  
        "start": "2020-01-01"  
      }  
    }  
  ]  
}
```

#### Explanation

* **resourceType**: The type of FHIR resource. Here, it is Group.
* **id**: The unique identifier for this instance of the Group resource.
* **identifier**: List of unique identifiers assigned to the Group.
* **type**: Specifies the type of entities included in the group (person in this case).
* **actual**: Indicates the group's type; true denotes an actual group.
* **code**: Optional field describing the purpose or use of the group.
* **name**: Human-readable name for the Group.
* **quantity**: Number of members in the Group.
* **member**: List of members within the group, each including an entity reference and optionally the period during which they were part of the group.

<br />

### Export

The FHIR $export operation is used to initiate the export of data from a FHIR server. When applied to the Group resource, the /Group/$export operation exports data for all members of a specified group. This is particularly useful for population health management, reporting, and other analytics purposes where you need to work with data for a defined group of patients or other entities.

#### Key Components of the /Group/$export Endpoint

1. **Parameters**:

* outputFormat (optional): Specifies the format of the exported data (e.g., application/fhir+ndjson).
* since (optional): Exports only data updated after the specified time.
* \_type (optional): Specifies the types of resources to be included in the export.

2. **Request**:\
   The export request is typically a GET request sent to the endpoint. It may include optional query parameters to filter or specify the exported data.
3. **Response**:\
   On successful initiation of the export, the server responds with an HTTP 202 Accepted status code and a Content-Location header. The Content-Location header provides the URL of the status endpoint where the client can check the progress of the export operation.

```
HTTP/1.1 202 Accepted
Content-Location: [polling-url]
```

<br />

#### Example Usage

Assume your FHIR base URL is `https://example.com/fhir`, and you want to export data for a Group with ID 123.\
**Example Request URL**:\
`https://example.com/fhir/Group/123/$export`\
**Example Response**:

```
http  
HTTP/1.1 202 Accepted  
Content-Location: <https://example.com/fhir/bulkstatus/xyz>
```

<br />

#### Step-by-Step Process

1. **Initiate Export**: 

```
GET https://example.com/fhir/Group/123/$export
```

2. **Check Export Status**:\
   Use the URL provided in the Content-Location header to poll the status of the export job:

```
GET https://example.com/fhir/bulkstatus/xyz
```

3. **Retrieve Exported Data**:\
   Once the job is complete, the status endpoint will provide URLs to download the exported files.
