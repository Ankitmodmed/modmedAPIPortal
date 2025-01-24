---
title: Device
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
Base profile: [http://hl7.org/fhir/us/core/StructureDefinition/us-core-implantable-device](http://hl7.org/fhir/us/core/StructureDefinition/us-core-implantable-device)

The Device resource tracks individual devices and their locations, records device usage (e.g., in procedures or observations), supports prescribing and dispensing, and manages Unique Device Identifier (UDI) information, such as for patient implants.

Read more from : [https://hl7.org/fhir/R4/device.html](https://hl7.org/fhir/R4/device.html)

**Sample Response Object:**

```json json
{
  "resourceType" : "Device",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // Instance identifier
  "definition" : { Reference(DeviceDefinition) }, // The reference to the definition for the device
  "udiCarrier" : [{ // Unique Device Identifier (UDI) Barcode string
    "deviceIdentifier" : "<string>", // Mandatory fixed portion of UDI
    "issuer" : "<uri>", // UDI Issuing Organization
    "jurisdiction" : "<uri>", // Regional UDI authority
    "carrierAIDC" : "<base64Binary>", // UDI Machine Readable Barcode String
    "carrierHRF" : "<string>", // UDI Human Readable Barcode String
    "entryType" : "<code>" // barcode | rfid | manual +
  }],
  "status" : "<code>", // active | inactive | entered-in-error | unknown
  "statusReason" : [{ CodeableConcept }], // online | paused | standby | offline | not-ready | transduc-discon | hw-discon | off
  "distinctIdentifier" : "<string>", // The distinct identification string
  "manufacturer" : "<string>", // Name of device manufacturer
  "manufactureDate" : "<dateTime>", // Date when the device was made
  "expirationDate" : "<dateTime>", // Date and time of expiry of this device (if applicable)
  "lotNumber" : "<string>", // Lot number of manufacture
  "serialNumber" : "<string>", // Serial number assigned by the manufacturer
  "deviceName" : [{ // The name of the device as given by the manufacturer
    "name" : "<string>", // R!  The name of the device
    "type" : "<code>" // R!  udi-label-name | user-friendly-name | patient-reported-name | manufacturer-name | model-name | other
  }],
  "modelNumber" : "<string>", // The model number for the device
  "partNumber" : "<string>", // The part number of the device
  "type" : { CodeableConcept }, // The kind or type of device
  "specialization" : [{ // The capabilities supported on a  device, the standards to which the device conforms for a particular purpose, and used for the communication
    "systemType" : { CodeableConcept }, // R!  The standard that is used to operate and communicate
    "version" : "<string>" // The version of the standard that is used to operate and communicate
  }],
  "version" : [{ // The actual design of the device or software version running on the device
    "type" : { CodeableConcept }, // The type of the device version
    "component" : { Identifier }, // A single component of the device version
    "value" : "<string>" // R!  The version text
  }],
  "property" : [{ // The actual configuration settings of a device as it actually operates, e.g., regulation status, time properties
    "type" : { CodeableConcept }, // R!  Code that specifies the property DeviceDefinitionPropetyCode (Extensible)
    "valueQuantity" : [{ Quantity }], // Property value as a quantity
    "valueCode" : [{ CodeableConcept }] // Property value as a code, e.g., NTP4 (synced to NTP)
  }],
  "patient" : { Reference(Patient) }, // Patient to whom Device is affixed
  "owner" : { Reference(Organization) }, // Organization responsible for device
  "contact" : [{ ContactPoint }], // Details for human/organization for support
  "location" : { Reference(Location) }, // Where the device is found
  "url" : "<uri>", // Network address to contact device
  "note" : [{ Annotation }], // Device notes and comments
  "safety" : [{ CodeableConcept }], // Safety Characteristics of Device
  "parent" : { Reference(Device) } // The parent device
}
```

This response provides essential details such as the device type, manufacturer, model, operational status, and associations with patient and location.