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
Base profile: <https://hl7.org/fhir/R4/patient.html>

### Common Use Cases

- Retrieve all patients for a specific practice
- Search for a specific patient
- Identify changes made within a given time frame
- Retrieve a patient's demographic information  
  Create a new patient record
- Update an existing patient’s demographic details

### Important Considerations

- Patient Creation: If your application uses the Patient CREATE resource, the API will allow the creation of new patient records. Be mindful of avoiding duplicate entries for patients already in the system.
- Patient Matching: To minimize duplicate patient records, ensure that your application at least matches on the following key identifiers: 
  - First name
  - Last name
  - Date of birth (DOB)
  - Gender  
    Additional recommended matching criteria include:
  - Email address
  - Phone number
  - Zip code
  - Social Security Number (SSN) (if applicable)

### Data Format

- All responses are returned in JSON by default. If you prefer XML, simply include the following parameter in your query:  
  `?_format=application/fhir+xml`

The following attributes are supported:

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Notes",
    "0-0": "id",
    "0-1": "The MMI-specific unique identifier for the patient",
    "1-0": "identifier",
    "1-1": "Lists the various identifiers of a patient.  \nA patient may have one, many, or all of the following identifiers:  \n  \n- **PMS** : (Practice Management System ID) - Note: For practices using Modernizing Medicine’s Practice Management System, this will be the MMI PMS ID. For practices using another Practice Management System, this will be the ID from that system.\n- **MRN** : <https://hl7.org/fhir/R4/v2/0203/index.html#v2-0203-MR>\n- **SSN** : <http://hl7.org/fhir/sid/us-ssn>**Note: **If you pass a header of ‘Content-Flag’ with a value of ‘Referral’ you can view this information (if it exists) for the Patient.  \n  **Referral Source** :  /fhir/v2/ValueSet/referral-source (populates only when Content-Flag: Referral is sent)",
    "2-0": "active",
    "2-1": "true|false",
    "3-0": "name",
    "3-1": "- family\n- given",
    "4-0": "telecom",
    "4-1": "The various contact methods for the patient. “rank” is used to determine the Patient’s preferred contact method.",
    "5-0": "gender",
    "5-1": "The Patient’s birth gender",
    "6-0": "birthDate",
    "6-1": "The Patient’s birth date",
    "7-0": "deceasedBoolean",
    "7-1": "true/false",
    "8-0": "address",
    "8-1": "The Patient’s address(es)",
    "9-0": "maritalStatus",
    "9-1": "The Patient’s Marital Status - <http://www.hl7.org/fhir/v2/0002/>",
    "10-0": "contact",
    "10-1": "Emergency Contact - <http://www.hl7.org/fhir/v2/0131/>",
    "11-0": "communication",
    "11-1": "Language - <http://www.loc.gov/standards/iso639-2/php/code_list.php>",
    "12-0": "extension - Race",
    "12-1": "<http://hl7.org/fhir/us/core/STU3.1/StructureDefinition-us-core-race.html>",
    "13-0": "extension - Ethnicity",
    "13-1": "<http://hl7.org/fhir/us/core/StructureDefinition/us-core-ethnicity>",
    "14-0": "generalPractitioner",
    "14-1": "<http://hl7.org/fhir/valueset-encounter-participant-type.html>  \nMMI will support:  \n  \n- REF Referrer : This is typically a referring physician and will reference an NPI if there is one in the system\n- PPRF Primary Performer : This is typically the patient’s Primary Practitioner at the practice and  \n    will be a reference to the /Practitioner  \n  **Note:** These are the values at the Patient level - meaning that these values are general. You may find different Primary and Referring practitioners at the Encounter level as many times those are specific to an individual encounter.**Note:** When Content-Flag: Referral is sent in the FHIR request, if the Patient has a ‘Referring Provider’, there will be a reference to a Practitioner within this field.",
    "15-0": "generalPractitioner extension - date last seen",
    "15-1": "The last visit date of the patient with the referenced provider. Added as an extension to the generalPractitioner field using a url of “date-last-seen”.",
    "16-0": "referral-source",
    "16-1": "Note: When Content-Flag: Referral is sent in the FHIR request, if the Patient has a ‘Referral Source’, there will be a reference to a Practitioner within this field.  \nIf the Patient has been assigned a Referral Source in MMPM, this will be a reference to that ID. Referral Sources can be found by querying the following Value Set: {baseurl}/{firm_url_prefix}/ema/fhir/v2/ValueSet/referral-source"
  },
  "cols": 2,
  "rows": 17,
  "align": [
    "left",
    "left"
  ]
}
[/block]


**Note: **The Patient resource also supports the following extensions:

- Patient Race: <http://hl7.org/fhir/us/core/STU3/StructureDefinition-us-core-race.html>
- Patient Ethnicity: <http://hl7.org/fhir/us/core/STU3/StructureDefinition-us-core-ethnicity.html>

The Following Operations are supported:

- Patient READ
- Patient SEARCH
- Patient CREATE
- Patient UPDATE