---
title: Value Sets
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
In many cases, certain values, such as customizable settings, are specific to a firm. For example, a practice's appointment types are often unique to that practice.

To manage this, we’ve created ValueSets for such firm-specific information. You can retrieve a firm's ValueSets by using the following request structure:

```Text http
GET {base_url}/{firm_url_prefix}/ema/fhir/v2/ValueSet
```

Where relevant, the corresponding ValueSet will also be included in the documentation for specific resources, though not all resources may require these values.