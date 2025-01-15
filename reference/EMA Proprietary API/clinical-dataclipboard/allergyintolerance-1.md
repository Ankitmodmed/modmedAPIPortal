---
title: AllergyIntolerance
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
Base profile: [https://www.hl7.org/fhir/allergyintolerance.html](https://www.hl7.org/fhir/allergyintolerance.html)

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
        clinicalStatus
      </td>

      <td style={{ textAlign: "left" }}>
        active | inactive | resolved
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        MMI uses several sources to populate Allergies in EMA. RxNorm is used for medication allergies.\
        You may see additional codes returned for other allergy types.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        patient
      </td>

      <td style={{ textAlign: "left" }}>
        Reference to Patient
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        onset  

        * onsetDateTime
        * lastOccurrence
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        recordedDate
      </td>

      <td style={{ textAlign: "left" }}>
        Date Recorded
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reaction
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reaction.manifestation
      </td>

      <td style={{ textAlign: "left" }}>
        Anaphylaxis (417516000) |Angioedema(41291007)|Diarrhea(62315008)|Dizziness( 404640003)|Fatigue(84229001)|GI upset(162059005)| Hives(126485001)|Liver toxicity (197354009)|Nausea(422587007)|Rash (162415008)|Shortness of breath(267036007)|Swelling(65124004)|Weal(247472004)|Other(419199007) - SNOMED CT (these are mapped in EMA)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reaction.severity
      </td>

      <td style={{ textAlign: "left" }}>
        unspecified|mild|mild to moderate|moderate|moderate to severe|severe|fatal - Use SNOMED CT\
        PLEASE NOTE: Since FHIR only supports mild|moderate|severe, EMA fields are mapped as followed:    

        * unspecified : will return no value  
        * mild=mild  
        * mild to moderate = mild  
        * moderate =moderate  
        * moderate to severe = moderate  
        * severe = severe  
        * fatal = severe
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reaction.substance
      </td>

      <td style={{ textAlign: "left" }}>
        code
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reaction.description
      </td>

      <td style={{ textAlign: "left" }}>
        narrative text box
      </td>
    </tr>
  </tbody>
</Table>

The Following Operations are supported:

* AllergyIntolerance READ
* AllergyIntolerance SEARCH
* AllergyIntolerance CREATE
* AllergyIntolerance UPDATE

***

### AllergyIntolerance CREATE

Note that Allergies added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.

***

### AllergyIntolerance UPDATE

Note that Allergies added or updated through the API will need to be reconciled by the Practice before those additions or changes will be added to the Patient’s chart. There is a UI to handle this on the front end.
