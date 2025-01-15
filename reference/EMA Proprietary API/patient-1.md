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
Base profile: [https://hl7.org/fhir/R4/patient.html](https://hl7.org/fhir/R4/patient.html)

### Common Use Cases

* Retrieve all patients for a specific practice
* Search for a specific patient
* Identify changes made within a given time frame
* Retrieve a patient's demographic information\
  Create a new patient record
* Update an existing patient’s demographic details

### Important Considerations

* Patient Creation: If your application uses the Patient CREATE resource, the API will allow the creation of new patient records. Be mindful of avoiding duplicate entries for patients already in the system.
* Patient Matching: To minimize duplicate patient records, ensure that your application at least matches on the following key identifiers: 
  * First name
  * Last name
  * Date of birth (DOB)
  * Gender\
    Additional recommended matching criteria include:
  * Email address
  * Phone number
  * Zip code
  * Social Security Number (SSN) (if applicable)

### Data Format

* All responses are returned in JSON by default. If you prefer XML, simply include the following parameter in your query:\
  `?_format=application/fhir+xml`

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
        The MMI-specific unique identifier for the patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identifier
      </td>

      <td style={{ textAlign: "left" }}>
        Lists the various identifiers of a patient.\
        A patient may have one, many, or all of the following identifiers:  

        * **PMS** : (Practice Management System ID) - Note: For practices using Modernizing Medicine’s Practice Management System, this will be the MMI PMS ID. For practices using another Practice Management System, this will be the ID from that system.
        * **MRN** : [https://hl7.org/fhir/R4/v2/0203/index.html#v2-0203-MR](https://hl7.org/fhir/R4/v2/0203/index.html#v2-0203-MR)
        * **SSN** : [http://hl7.org/fhir/sid/us-ssn](http://hl7.org/fhir/sid/us-ssn)**Note:**If you pass a header of ‘Content-Flag’ with a value of ‘Referral’ you can view this information (if it exists) for the Patient.  
          * \*Referral Source\*\* :  /fhir/v2/ValueSet/referral-source (populates only when Content-Flag: Referral is sent)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        active
      </td>

      <td style={{ textAlign: "left" }}>
        true|false
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        * family
        * given
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        telecom
      </td>

      <td style={{ textAlign: "left" }}>
        The various contact methods for the patient. “rank” is used to determine the Patient’s preferred contact method.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        gender
      </td>

      <td style={{ textAlign: "left" }}>
        The Patient’s birth gender
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        birthDate
      </td>

      <td style={{ textAlign: "left" }}>
        The Patient’s birth date
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        deceasedBoolean
      </td>

      <td style={{ textAlign: "left" }}>
        true/false
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        address
      </td>

      <td style={{ textAlign: "left" }}>
        The Patient’s address(es)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        maritalStatus
      </td>

      <td style={{ textAlign: "left" }}>
        The Patient’s Marital Status - [http://www.hl7.org/fhir/v2/0002/](http://www.hl7.org/fhir/v2/0002/)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contact
      </td>

      <td style={{ textAlign: "left" }}>
        Emergency Contact - [http://www.hl7.org/fhir/v2/0131/](http://www.hl7.org/fhir/v2/0131/)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        communication
      </td>

      <td style={{ textAlign: "left" }}>
        Language - [http://www.loc.gov/standards/iso639-2/php/code\_list.php](http://www.loc.gov/standards/iso639-2/php/code_list.php)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        extension - Race
      </td>

      <td style={{ textAlign: "left" }}>
        [http://hl7.org/fhir/us/core/STU3.1/StructureDefinition-us-core-race.html](http://hl7.org/fhir/us/core/STU3.1/StructureDefinition-us-core-race.html)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        extension - Ethnicity
      </td>

      <td style={{ textAlign: "left" }}>
        [http://hl7.org/fhir/us/core/StructureDefinition/us-core-ethnicity](http://hl7.org/fhir/us/core/StructureDefinition/us-core-ethnicity)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        generalPractitioner
      </td>

      <td style={{ textAlign: "left" }}>
        [http://hl7.org/fhir/valueset-encounter-participant-type.html](http://hl7.org/fhir/valueset-encounter-participant-type.html)\
        MMI will support:  

        * REF Referrer : This is typically a referring physician and will reference an NPI if there is one in the system
        * PPRF Primary Performer : This is typically the patient’s Primary Practitioner at the practice and\
            will be a reference to the /Practitioner  
          * \*Note:**These are the values at the Patient level - meaning that these values are general. You may find different Primary and Referring practitioners at the Encounter level as many times those are specific to an individual encounter.**Note:\*\* When Content-Flag: Referral is sent in the FHIR request, if the Patient has a ‘Referring Provider’, there will be a reference to a Practitioner within this field.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        generalPractitioner extension - date last seen
      </td>

      <td style={{ textAlign: "left" }}>
        The last visit date of the patient with the referenced provider. Added as an extension to the generalPractitioner field using a url of “date-last-seen”.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        referral-source
      </td>

      <td style={{ textAlign: "left" }}>
        Note: When Content-Flag: Referral is sent in the FHIR request, if the Patient has a ‘Referral Source’, there will be a reference to a Practitioner within this field.\
        If the Patient has been assigned a Referral Source in MMPM, this will be a reference to that ID. Referral Sources can be found by querying the following Value Set: \{baseurl}/\{firm\_url\_prefix}/ema/fhir/v2/ValueSet/referral-source
      </td>
    </tr>
  </tbody>
</Table>

**Note:** The Patient resource also supports the following extensions:

* Patient Race: [http://hl7.org/fhir/us/core/STU3/StructureDefinition-us-core-race.html](http://hl7.org/fhir/us/core/STU3/StructureDefinition-us-core-race.html)
* Patient Ethnicity: [http://hl7.org/fhir/us/core/STU3/StructureDefinition-us-core-ethnicity.html](http://hl7.org/fhir/us/core/STU3/StructureDefinition-us-core-ethnicity.html)

The Following Operations are supported:

* Patient READ
* Patient SEARCH
* Patient CREATE
* Patient UPDATE
