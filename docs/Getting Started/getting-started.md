---
title: Getting Started
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
If you are looking to get started developing an integration or an application for a ModMed customer, you have come to the right place.  The most important part of this process is understanding what problem you are trying to solve for your customer and then understanding the available mechanisms to be able to solve that problem.  

As mentioned previously, the EMA Proprietary API is an API that will allow a third party developer the ability to work with specific capabilities inside of ModMed EMA® and ModMed Practice Management systems.  This API allows for READ, SEARCH, CREATE, and UPDATE Functionality for many resources and is likely the best mechanism to be able to help solve more "operational" problems for our mutual customers.  Typically, this is where 3rd Party systems and vendors come to become a part of the [synapSYS Marketplace ](https://modmed.my.site.com/synapsysmarketplace/s/) .  Creating an application through this program will provide vendors with a backend "sandbox" to develop an application against.  Vendors will develop their application working with the synapSYS team to understand which ACLs (access to resources) they will need to power their application.  Once the application is developed, the vendor will meet with the synapSYS team for a technical review before they are permitted to gain access to their first customer's production system.  If this program is of interest to you, please visit: https://portal.api.modmed.com/docs/ema-proprietary-api

The Certified FHIR API is an API that leverages the FHIR healthcare standard and is able to connect to both ModMed EHRs: EMA (for all non-GI specialities), and gGastro.  This API  leverages SMART on FHIR technology designed to be able to quickly connect our customers, Providers, and Patients to the world of healthcare applications available to them.  Currently this API supports READ and SEARCH only (no WRITE capabilities) + Bulk FHIR.  This system involves understanding that under the 21st Century Cures Act and the HTI regulations following specify that EHRs must make their customers' endpoints [publicly available](https://mm-fhir-endpoint-display.prod.fhir.ema-api.com/) , leveraging those endpoints in standard ways to understand the capabilities of the system, and then registering an app (ClientId) to grant the scopes and capabilities necessary for an app to connect to our customers.  This is a more "self-service" mechanism.  If this is of interest to you, please check out: https://portal.api.modmed.com/docs/register-to-become-a-modmed-certified-fhir-api-vendor

Additionally, depending on what your capabilities are, you may be interested in more traditional HL7.   ModMed EMA®, ModMed Practice Management, and gGastro all have various HL7 capabilities and standard ways in which they can be leveraged.  Please reach out to synapsys@modmed.com for more information on our HL7 capabilities.  

Lastly, for vendors visiting this site looking for other mechanisms, our EHRs have other native interoperable capabilities such as DirectMail which can automate the sending of CCD and Visit Note information to outside systems in a variety of ways.  
