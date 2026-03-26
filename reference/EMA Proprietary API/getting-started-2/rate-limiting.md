---
title: Rate Limiting
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
By default, each API key is limited to 1250 calls per minute. That translates to roughly 20 calls per second.  We strongly recommend throttling your requests to stay well within the 20-call-per-second threshold. This ensures optimal system stability and prevents your application from encountering rate-limiting (429) errors during high-volume bursts.  So it is expected that you will stagger your calls in such a way as to not get rate limited by what is in place.  If your application requires more frequent calls, please reach out to the person who provisioned your credentials and set up a call to understand your needs. Support email: [synapsys@modmed.com](mailto:synapsys@modmed.com)
