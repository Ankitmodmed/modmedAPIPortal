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

Group represents a defined collection of entities that may be discussed or acted upon collectively but which are not expected to act collectively, and are not formally or legally recognized; i.e. a collection of entities that isn't an Organization.

Read more from: [https://hl7.org/fhir/group.html](https://hl7.org/fhir/group.html)

#### **Sample Response Object**

```json json
{
  "resourceType" : "Group",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Business Identifier for this Group
  "active" : <boolean>, // Whether this group's record is in active use
  "type" : "<code>", // R!  person | animal | practitioner | device | careteam | healthcareservice | location | organization | relatedperson | specimen
  "membership" : "<code>", // R!  definitional | enumerated
  "code" : { CodeableConcept }, // Kind of Group members
  "name" : "<string>", // Label for Group
  "description" : "<markdown>", // Natural language description of the group
  "quantity" : "<unsignedInt>", // Number of members
  "managingEntity" : { Reference(Organization|Practitioner|PractitionerRole|
   RelatedPerson) }, // Entity that is the custodian of the Group's definition
  "characteristic" : [{ // Include / Exclude group members by Trait
    "code" : { CodeableConcept }, // R!  Kind of characteristic
    // value[x]: Value held by characteristic. One of these 5:
    "valueCodeableConcept" : { CodeableConcept },
    "valueBoolean" : <boolean>,
    "valueQuantity" : { Quantity },
    "valueRange" : { Range },
    "valueReference" : { Reference },
    "exclude" : <boolean>, // R!  Group includes or excludes
    "period" : { Period } // Period over which characteristic is tested
  }],
  "member" : [{ // Who or what is in group
    "entity" : { Reference(CareTeam|Device|Group|HealthcareService|Location|
    Organization|Patient|Practitioner|PractitionerRole|RelatedPerson|Specimen) }, // R!  Reference to the group member
    "period" : { Period }, // Period member belonged to the group
    "inactive" : <boolean> // If member is no longer in group
  }]
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
**Example Request URL**:
`https://example.com/fhir/Group/123/$export`
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