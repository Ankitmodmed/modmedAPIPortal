---
title: Header Flags
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
To ensure API changes remain non-breaking for our vendors, we sometimes use header flags to control the content returned in certain payloads. To access specific content, include the following header in your request:

* `Content-flag`

**Available Header Flag Values:**

* `Referral:` Adds Referral Contact and Referral Source information to the Patient and Appointment payloads.
* `Pagination_optimization_disabled:` Provides the total count for all resources, not just the current page.