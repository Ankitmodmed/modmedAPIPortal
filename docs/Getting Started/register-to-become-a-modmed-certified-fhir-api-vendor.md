---
title: Become a ModMed Certified FHIR API Vendor
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
Before Registering to become a Certified FHIR API vendor, please review the following guide to assist you in understanding the type of application you would like to build, the scopes and capabilities, and the way that customers, Providers, and Patients will interact with your application. 

Once you register to become a Certified FHIR API vendor, you will be prompted with a screen to configure your app.  And it is important to know what decisions you'll need to make before registering the app.  

**App Type**

If you are working with a practice and you require access to their providers and patients' clinical data at the practice level, it is recommended that you create a Bulk FHIR application. This allows an Admin at the practice to add your ClientId to their practice one time to be able to gain access to that data as needed.  All other app types will require either a Provider (defined as a role at the practice who has access to Clinical patient data) for all Provider apps or a Patient (defined as a user who has access to their clinical data through a Patient Portal username and password) for all Patient apps to authenticate themselves.  And the vendor must provide that mechanism for initial use.  Once a Standalone flow is used to authenticate the patient or provider, then a link will be placed into their UI for them to use the app as designed from inside the EHR.  

For 'Patient' apps, it will require a Patient at the practice (with valid username/password for their patient portal access) to authenticate.  Once they have authenticated, a link will be placed inside their portal for repeated access to your application and/or for the Patient to manage or disable access.  

For 'Provider' apps, it will require a Provider at the practice to authenticate with the same credentials they use to authenticate to the EHR.  Once they have authenticated, a link will be placed inside their EHR instance (different places depending on scopes) for them to leverage right from inside the EHR.  

You can also create a 'Patient and Provider' app which can handle auth for both Patients and Providers.  

**Scopes**

Context scopes — control what gets put in the token

| Scope            | Standalone              | EHR Launch                      | What it does                                        |
| :--------------- | :---------------------- | :------------------------------ | :-------------------------------------------------- |
| launch/patient   | Triggers patient picker | Passes patient from EHR context | Puts patient claim in the token                     |
| launch/encounter | Rarely useful           | Passes encounter from EHR       | Puts encounter claim in token                       |
| launch           | Never                   | Always required                 | Tells auth server to honor the EHR's launch context |

<br />

Identity scopes — control what you know about the logged-in user

| Scope    | When to use                                          | What it does                                                       |
| :------- | :--------------------------------------------------- | :----------------------------------------------------------------- |
| openid   | Always                                               | Required for OIDC — enables id_token                               |
| profile  | When you need user name/email                        | Adds basic profile claims to id_token                              |
| fhirUser | When you need to look up the user as a FHIR resource | Adds a fhirUser claim — a URL like Practitioner/abc123 you can GET |

<br />

Session scopes — control token lifetime

| Scope          | When to use                  | What it does                                                |
| :------------- | :--------------------------- | :---------------------------------------------------------- |
| online_access  | Most apps                    | Refresh token that expires when the user's EMA session ends |
| offline_access | Background/long-running apps | Refresh token that doesn't expire with the session          |

Resource scopes — control what FHIR data you can read

| Scope               | When to use           | What it does                                                                                  |
| :------------------ | :-------------------- | :-------------------------------------------------------------------------------------------- |
| patient/Resource.rs | Patient context apps  | Read/search that resource scoped to the token's patient — can't read other patients' data     |
| user/Resource.rs    | Provider context apps | Read/search that resource as the logged-in user — broader access across patients they can see |

By App Type

| App Type                        | Required                                         | Makes sense                                     | Doesn't make sense                  |
| :------------------------------ | :----------------------------------------------- | :---------------------------------------------- | :---------------------------------- |
| Standalone (patient picker)     | openid, launch/patient                           | fhirUser, online_access, patient/*.rs           | launch, launch/encounter, user/*.rs |
| EHR Launch — Patient            | openid, launch, launch/patient                   | fhirUser, online_access, patient/*.rs           | launch/encounter, user/*.rs         |
| EHR Launch — Provider           | openid, launch, launch/encounter                 | fhirUser, online_access, user/*.rs              | launch/patient, patient/*.rs        |
| EHR Launch — Patient + Provider | openid, launch, launch/patient, launch/encounter | fhirUser, online_access, patient/*.rs,user/*.rs | —                                   |
| Background / automated          | openid, offline_access                           | user/*.rs                                       | launch/patient, launch/encounter    |

<br />

<HTMLBlock>{`
<!DOCTYPE html>
<body>
    <div>
      <a href="https://fhir-vendor-dashboard.kube.prod.mmicse.com/"><button class="custom-link-button">Register Now</button></a>
  </div>
</body>
</html>
`}</HTMLBlock>
