---
title: DiagnosticReport (Results)
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
Base profile: &lt;https://www.hl7.org/fhir/diagnosticreport.html&gt;

DiagnosticReport can be used to find Results PDFs for patients in EMA.

The following attributes are supported:

| Field Name        | Notes                                                          |
| :---------------- | :------------------------------------------------------------- |
| id                |                                                                |
| lastUpdated       |                                                                |
| identifier        | Reference to the RequisitionID                                 |
| basedOn           | Reference to ServiceRequest                                    |
| status            | final\|preliminary\|correction\|partial                        |
| code              | Orderable Code - likely CPT, LOINC, or Compendium code         |
| subject           | Reference to Patient                                           |
| encounter         | Reference to Encounter                                         |
| effectiveDateTime | Date and Time the report was processed by the reporting entity |
| issued            | Date and Time the report was delivered to EMA                  |
| performer         | Performing Entity (whoever performed the study)                |
| presentedForm     | PDF or document of the report                                  |