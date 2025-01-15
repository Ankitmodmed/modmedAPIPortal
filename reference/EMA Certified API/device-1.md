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

FHIR (Fast Healthcare Interoperability Resources) Device endpoint is used to represent details about a physical device used in healthcare, such as a medical instrument or a piece of software.

### Key Components

**Device Resource**

* **Identifier**: Unique ID for the device.
* **Type**: What kind of device it is.
* **Manufacturer**: Who made the device.
* **Model**: Device model number.
* **Version**: Version number of the device.
* **Status**: Operational status of the device (available, not available, entered in error).
* **Patient**: Which patient the device is assigned to.
* **Location**: Where the device is located.

**Sample Response Object:**

```Text json
{  
    "resourceType": "Device",  
    "id": "example-device",  
    "identifier": [  
        {  
            "system": "http://hospital.smarthealthit.org/devices",  
            "value": "12345X"  
        }  
    ],  
    "type": {  
        "coding": [  
            {  
                "system": "http://snomed.info/sct",  
                "code": "86184003",  
                "display": "Electrocardiographic monitor and recorder"  
            }  
        ],  
        "text": "ECG monitor"  
    },  
    "manufacturer": "Acme Devices",  
    "model": "UltraECG 2000",  
    "version": "3.2",  
    "status": "available",  
    "patient": {  
        "reference": "Patient/example"  
    },  
    "location": {  
        "reference": "Location/1"  
    }  
}
```

This response provides essential details such as the device type, manufacturer, model, operational status, and associations with patient and location.
