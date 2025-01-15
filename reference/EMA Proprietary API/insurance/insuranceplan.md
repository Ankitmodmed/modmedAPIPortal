---
title: InsurancePlan
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
Currently the ‘InsurancePlan’ resource can only be used to query and find InsurancePlans in the ModMed Practice Management system. InsurancePlan information is optional when creating Coverage.

The following attributes are supported:

| Field Name    | Notes                                                                                                          |
| :------------ | :------------------------------------------------------------------------------------------------------------- |
| id            | ID of the InsurancePlan                                                                                        |
| \_count       | Number of records to use as the page size for paginated search. The maximum page size for this Resource is 100 |
| \_lastUpdated | Search by data/time of \_lastUpdated                                                                           |
| status        | active or inactive                                                                                             |
| name          | Name of the InsurancePlan                                                                                      |
| owned-by      | reference to Organization (payer)                                                                              |
| plan          | type of plan                                                                                                   |

The Following Operations are supported:

- InsurancePlan READ
- InsurancePlan SEARCH