---
title: Slot
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
Base Profile: &lt;https://www.hl7.org/fhir/slot.html&gt;

Common use cases include:

- Find available Slots for the purposes of booking an Appointment

The following attributes are supported:

| Field Name | Notes                                            |
| :--------- | :----------------------------------------------- |
| id         | GUID for the Slot                                |
| identifier | - Location   - Practitioner   - appointment-type |
| schedule   | display text                                     |
| status     |                                                  |
| start      | start time and date                              |
| end        | end time and date                                |

The Following Operations are supported:

- Slot SEARCH

**Note:** 

1. Slot Search is currently limited to 5 day increments. When looking for available slots please use time frames which are limited to 5 days or less.  
   Additionally, it is highly recommended that, while not required, you include at least one Practitioner and at least one Location in your query. Any query which does not contain those parameters may be unpredictable in terms of response times.
2. You cannot do a search with only a single date if the prefix is &lt;=, &lt;, >=, or >. Valid prefixes for the date search are only 'eq' or no prefix at all.