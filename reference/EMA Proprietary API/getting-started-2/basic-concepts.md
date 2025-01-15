---
title: Basic Concepts
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
This API simulates the behavior of a user within a medical practice. Once your application is approved, each practice you wish to collaborate with (or that wants to collaborate with you) must grant your application access by generating unique credentials. These credentials are specific to each practice, and you will use them to authenticate your application with that particular practice.

It's recommended that your application be capable of storing unique credentials for every practice it interacts with. Each MMI practice also has a unique URL structure, distinguished by a practice-specific prefix. The URL format follows this structure:

https\://{practice_prefix}.ema.md

For example:

- "Dermatology Associates" might have a URL like <https://dermassoc.ema.md>
- "Urological Associates" might have a URL like <https://uroassoc.ema.md>

Your application must support this URL prefix system to differentiate between MMI practices.

***

### **EMA vs MMPM**

Before integrating with Modernizing Medicine, it's important to determine whether your application will rely on Practice Management data, Clinical data, or both. Practices may use either Electronic Medical Assistant (EMA) or Modernizing Medicine Practice Management (MMPM). Ensure the practice has the necessary products to support your application's functionality. Key differences to be aware of:

EMA-only practices will not have:

- Appointment or scheduling information (available only in the Practice Management system).
- Patient account balances.
- The ability to process inbound charges.
- Charges available until the visit is finalized.

***

### **Identifiers Overview**

Handling identifiers correctly is crucial when interacting with the API. Here’s what you need to know:

#### Patients

Every patient has a unique MMI Identifier (commonly referred to as EMAID).  
Some patients may also have a PMSID if they interface with another Practice Management System.  
Patients will also have a Medical Record Number (MRN). However, non-MMI identifiers (e.g., PMSID, MRN) cannot be guaranteed as unique.

#### Practitioners(Providers)

Providers have a unique MMI identifier and an NPI (National Provider Identifier). Providers from other Practice Management Systems may also have a PMSID. If your application processes charges, you'll often need the Provider's NPI to map the charge to the Billing Provider’s Business Unit in MMPM.

#### Locations or Business Units

Locations and Business Units each have unique MMI identifiers. They may also have a PMSID and/or NPI.  
Make sure that your application retrieves the necessary identifiers from the API to handle these transactions appropriately.