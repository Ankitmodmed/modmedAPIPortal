---
title: Create Referring Practitioner
excerpt: ''
api:
  file: ema-proprietary-api.json
  operationId: post_practitioner
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
**Note:** EMA supports two type of Practitioners. Practitioner CREATE is currently only supported to create Referring Providers into a Practice. You cannot update or create any of the practice’s users or providers, only Referring Providers.

| Name          | Type   | Description                                                   |
| :------------ | :----- | :------------------------------------------------------------ |
| family        | string | This is the practitioner’s last name - Supports exact matches |
| given         | string | The given name of the practitioner                            |
| telecom       | string | The telecom details for a Practitioner                        |
| address       | string | The address of the Practitioner                               |
| qualification | string | The speciality (specialities) of the Practitioner             |
