---
title: Count and Pagination
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
For performance optimization, some API endpoints return paginated responses. You can control pagination with two optional parameters:

* **\_count:** Specifies the number of results per page. If not provided, the default maximum page size for the resource will be used. For example, the current maximum page size for the Patient resource is 50.
* **page:** Specifies the page number to retrieve in the paginated results.

### Pagination Behavior

We support two different implementations for handling pagination and result counts. As of release 7.7, by default:

* total represents the total number of results on the current page.
* next provides the link to the next set of results.

Pagination continues until no more results are available (i.e., when total is 0).

```
"resourceType": "Bundle",
"id": "3fdfc58b-214c-45c4-94f5-c1fe0dd5b3cb",
"meta": {
	"lastUpdated": "2024-05-24T13:43:18.566+00:00"
},
"type": "searchset",
"total": 50,
"link": [
  {
    "relation": "self",
    "url": "{base url}/{firm_url_prefix/ema/fhir/v2/Patient"
  },
  {
    "relation": "next",
    "url": "{base url}/{firm_url_prefix/ema/fhir/v2/Patient?page=2"
  }
],
```

An alternative implementation is available that provides the total number of records and calculates the total number of pages in advance. However, this method is more resource-intensive and may result in slower response times. It is recommended to use this option only when necessary.

**Enabling Alternative Pagination**\
To enable this implementation, include the following header in your request:

* `Content-flag: Pagination_optimization_disabled`

When this header is present, the response will include paginated links in the returned bundle, providing links for both the next and previous pages. However, not all links may be returned depending on the context. For example, if only one page of records exists, no pagination links will be provided.

**Example of Paginated Links in the Payload**\
The response payload will include pagination links, formatted as follows:

```
{
  "resourceType": "Bundle",
  "id": "3fdfc58b-214c-45c4-94f5-c1fe0dd5b3cb",
  "meta": {
    "lastUpdated": "2024-05-24T13:43:18.566+00:00"
  },
  "type": "searchset",
  "total": 22437,
  "link": [
    {
      "relation": "self",
      "url": "{base url}/{firm_url_prefix/ema/fhir/v2/Patient"
    },
    {
      "relation": "next",
      "url": "{base url}/{firm_url_prefix/ema/fhir/v2/Patient?page=2"
    },
    {
      "relation": "last",
      "url": "{base url}/{firm_url_prefixr/ema/fhir/v2/Patient?page=449"
    }
  ],
```

Note that the "self" link is always returned. The self link is the url that was requested by the user.\
**Note:** The ‘Slot’ resource does not have any pagination.
