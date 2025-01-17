---
title: Development Basics
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
Once your generic sandbox has been provisioned, you will receive an email with the credentials and details needed to begin development. These credentials include a **Username**, **Password**, and **Key**. Using these, you can generate Access and Refresh tokens via the OAuth2 "Password Grant" endpoint (see the "[Authentication](https://emasample.readme.io/reference/authentication)" section).

# Environment Keys

The specific key you use depends on the environment:

* **Staging/Development:** `https://stage.ema-api.com/ema-dev/firm/`
* **Training:** `https://stage.ema-api.com/ema-training/firm/`
* **Production:**` https://mmapi.ema-api.com/ema-prod/`

You will not receive a production key until you have completed the required steps outlined below. Include the key in the header for all API calls: `x-api-key={key}`.

By default, your sandbox environment provides access to **all resources** so you can explore the full capabilities of the API.

# Requesting Resources

Once development is nearing completion, you'll need to inform ModMed which specific resources your application requires to go live. Please note that resource provisioning can take up to two weeks after submission, so it’s important to submit your request in advance to avoid delays.

To register your application with ModMed, submit the following details to your MMI contact:

* Vendor Name
* Application Name
* Application Description
* Desired Resources: Specify the API resources your application requires (e.g., Patient READ/SEARCH, ChargeItem CREATE/READ/SEARCH, Practitioner READ/SEARCH, etc.).

**Final Review Process**\
When your application is ready, we will schedule a demo and technical review. The review typically includes:

* An **end-to-end demo** of your system.
* A **Proof of Concept** demonstration, showing full functionality within your sandbox.
* A **technical discussion** to review the API resources in use and how often they will be called.

Once the demo and technical discussion are successfully completed and your desired resources are provisioned, you will receive a **production key** and instructions on how to take practices live with your application.

***

# Endpoints

**Base URLs** - these will be referred to throughout the documentation as \{base\_url}

**Generic Sandboxes**\
[https://stage.ema-api.com/ema-dev/firm/](https://stage.ema-api.com/ema-dev/firm/)

**Practice Sandboxes**\
[https://stage.ema-api.com/ema-training/firm/](https://stage.ema-api.com/ema-training/firm/)

**Production**\
[https://mmapi.ema-api.com/ema-prod/firm](https://mmapi.ema-api.com/ema-prod/firm)

***

## Authentication

**Generic Sandboxes**\
[https://stage.ema-api.com/ema-dev/firm/(firm\_url\_prefix)/ema/ws/oauth2/grant](https://stage.ema-api.com/ema-dev/firm/\(firm_url_prefix\)/ema/ws/oauth2/grant)

**Practice Sandboxes**\
[https://stage.ema-api.com/ema-training/firm/(firm\_url\_prefix)/ema/ws/oauth2/grant](https://stage.ema-api.com/ema-training/firm/\(firm_url_prefix\)/ema/ws/oauth2/grant)

**Production**\
[https://mmapi.ema-api.com/ema-prod/firm/(firm\_url\_prefix)/ema/ws/oauth2/grant](https://mmapi.ema-api.com/ema-prod/firm/\(firm_url_prefix\)/ema/ws/oauth2/grant)

***

## Resources

**Generic Sandboxes**\
[https://stage.ema-api.com/ema-dev/firm/(firm\_url\_prefix)/ema/fhir/v2/\{Resource}](https://stage.ema-api.com/ema-dev/firm/\(firm_url_prefix\)/ema/fhir/v2/\{Resource})

**Practice Sandboxes**\
[https://stage.ema-api.com/ema-training/firm/(firm\_url\_prefix)/ema/fhir/v2/\{Resource}](https://stage.ema-api.com/ema-training/firm/\(firm_url_prefix\)/ema/fhir/v2/\{Resource})

**Production**\
[https://mmapi.ema-api.com/ema-prod/firm/(firm\_url\_prefix)/ema/fhir/v2/\{Resource}](https://mmapi.ema-api.com/ema-prod/firm/\(firm_url_prefix\)/ema/fhir/v2/\{Resource})

***

## Variables

**\{firm\_url\_prefix}** - this is the unique identifier for the specific firm (practice) you’ll be working with.

***

## Examples - Authentication

**Generic Sandbox Authentication**\
[https://stage.ema-api.com/ema-dev/firm/dermpmsandbox1/ema/ws/oauth2/grant](https://stage.ema-api.com/ema-dev/firm/dermpmsandbox1/ema/ws/oauth2/grant)

**Practice Sandbox Authentication**\
G5rWTGwOgB461tVmqUlDc3JUHCzoyURh6q25Td65
[https://stage.ema-api.com/ema-training/firm/dermassoc/ema/ws/oauth2/grant](https://stage.ema-api.com/ema-training/firm/dermassoc/ema/ws/oauth2/grant)

**Production Authentication**\
[https://mmapi.ema-api.com/ema-prod/firm/dermassoc/ema/ws/oauth2/grant](https://mmapi.ema-api.com/ema-prod/firm/dermassoc/ema/ws/oauth2/grant)

***

## Examples - Resources

**Generic Sandboxes - Patient**\
[https://stage.ema-api.com/ema-dev/firm/dermpmsandbox1/ema/fhir/v2/Patient](https://stage.ema-api.com/ema-dev/firm/dermpmsandbox1/ema/fhir/v2/Patient)

**Practice Sandboxes - Patient**\
[https://stage.ema-api.com/ema-training/firm/dermassoc/ema/fhir/v2/Patient](https://stage.ema-api.com/ema-training/firm/dermassoc/ema/fhir/v2/Patient)

**Production - Patient**\
[https://mmapi.ema-api.com/ema-prod/firm/dermassoc/ema/fhir/v2/Patient](https://mmapi.ema-api.com/ema-prod/firm/dermassoc/ema/fhir/v2/Patient)