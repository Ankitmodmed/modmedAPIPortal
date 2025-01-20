---
title: Introduction to MMI
deprecated: false
hidden: false
metadata:
  robots: index
---
MMI has several Clinical and Practice Management applications and systems. This API is here\
to support the ModMed GI platform, gGastro, as well as the ModMed EMA platform.

You can find the endpoints for our customers here:
[https://mm-fhir-endpoint-display.prod.fhir.ema-api.com/](https://mm-fhir-endpoint-display.prod.fhir.ema-api.com/)

If you have issues finding the right endpoint for your customer, you can send an email to
[synapsys@modmed.com](mailto:synapsys@modmed.com).
Apps built upon this platform can be built as the following types of applications:

1. **Patient App** - This means that in order to use this app, a Patient, who is a registered\
   user in one of MMI’s Customers’ Patient Portal, will need to authenticate with the same
   credentials they use to login to the Patient Portal, to use your application. Once
   authenticated, Patients will have a mechanism to Manage their apps (Revoke access)
   and launch their apps from inside the Patient Portal:

![](https://files.readme.io/f10675abdb8064833aeebd8c800b01d693dcc20a97a5c46b90c6a2d2505158f1-image.png)

2. **Provider App** - This means that in order to use this app, a Provider, who is a registered\
   provider in one of MMI’s gGastro or EMA systems, will need to authenticate with the
   same credentials they use to login to their EMR, to use your application. Once
   authenticated, Providers will have a mechanism to Manage their apps (Revoke access)
   or Launch their apps - depending on the type of app:
   **Pop health (ie. no Patient context):**

   <Image align="center" src="https://files.readme.io/f26b5acd473810968e41474f57d3fe9bf8a6e59748afb8c8d30cb0b5b4a82869-image.png" />

**Patient Context (inside of a patient’s chart):**

![](https://files.readme.io/a12e17b5714a105a565abfc17f11416d4f573af63837763b45922bc567513b62-image.png)

3. **Bulk App** - This type of app will require consent from the practice. A Practice can\
   provide your app consent by adding your app’s ClientID to their ‘Manage Bulk FHIR’
   section in their Admin section:

   ![](https://files.readme.io/daab964efb6b51780f82d056ff0f42e9d01dac166ac428d82356ee78579a7f23-image.png)

<br />

The general process for apps built upon the Certified FHIR API is as follows:

1. Register with MMI: [https://fhir-vendor-dashboard.kube.prod.mmicse.com/](https://fhir-vendor-dashboard.kube.prod.mmicse.com/)
2. Create an application:

   ![](https://files.readme.io/15350d1f41cd92c6dc6f9299ac15ae18971d721e86218abd4028d56954fa0454-image.png)
3. Your app will be created in a ‘Disabled’ state:

   ![](https://files.readme.io/e2a7a6ea2e342e8d5722f4c02b0842f56c264a407c246c6fd227ac41d3302076-image.png)
4. MMI will review new apps daily and Enable apps that are configured correctly. Once\
   your app is enabled, it will look like this:

   ![](https://files.readme.io/138d3e304a0c84fef314f11737dd9235966fe166db74281b7fa161b0c26eadc8-image.png)
5. For any Non-Bulk application, your customers should be able to use it. You will need to\
   provide the user (either a patient or a provider) with a mechanism (a link) to authenticate.
6. For Bulk applications, please refer to the Bulk App section above which explains the\
   process for a practice to consent to allowing your app to query for Bulk data.