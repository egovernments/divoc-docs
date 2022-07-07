---
description: Conversion utility for issuing a Smart Health Card (SHC) compliant QR code
---

# DIVOC’s SHC Adapter Service

## What will it cover?

* [Overview of the Smart **** Health Card specification](divocs-shc-adapter-service.md#overview-of-the-smart-health-card-specification)
* [What is DIVOC’s Smart Health Card adapter?](divocs-shc-adapter-service.md#what-is-divocs-shc-adapter-service)&#x20;
* [How does the conversion utility work?](divocs-shc-adapter-service.md#how-does-the-conversion-utility-work)&#x20;
* [References:](divocs-shc-adapter-service.md#references)&#x20;

&#x20;            \- [Technical specification](divocs-shc-adapter-service.md#technical-specification)

## **Overview of the Smart Health Card specification**

A Smart Health Card (SHC) is a globally popular HL7 FHIR (Fast Healthcare Interoperability Resources) and [**W3C verifiable credential standards**](https://www.w3.org/TR/vc-data-model/) - based open standard for generating tamper-proof health credentials.

* An SHC provides a framework that facilitates the generation, storing and verification of the SHC holder’s clinical information.
* To enable people to access a digital record of their COVID-19 vaccine history, SHCs ascertaining an individual’s vaccination and test result status, have been rolled out in US-States (California, Colorado, Connecticut, Delaware, Hawaii, Illinois, New York, and 9 others), Canada, and Japan.
* You can find the registry of verified Smart Health Card issuers for vaccinators **** [**here**](https://www.commontrustnetwork.org/verifier-list) **** and **** [**here**](https://smarthealth.cards/en/issuers.html).

| Information an SHC can contain         | Information an SHC cannot contain |
| -------------------------------------- | --------------------------------- |
| Legal name and date of birth           | Phone number                      |
| Clinical information                   | Address                           |
| Tests: Date, manufacturer, and result  | Government-issued identifier      |
| Vaccinations: type, date, and location | Any other health information      |

&#x20;                                          _(Information courtesy_ [_**SMART Health Card**_](https://smarthealth.cards/en/)_)_

* To understand how they work and where they can be used, click [**here**](https://smarthealth.cards/en/) and [**here**](https://smarthealthit.org/health-cards/).

## What is DIVOC’s SHC adapter service?

Besides it’s native COVID-19 certificate schema, the DIVOC platform has also developed an adapter service to convert a native DIVOC W3C-JSON certificate into a Smart Health Card-compliant QR code.

### **Need for the SHC-Adapter service**

* This utility was required to facilitate restriction-free international travel for residents from DIVOC’s adopter countries by enabling conversion of a DIVOC issued vaccine certificate to an SHC-QR code.
* The key design principles on which DIVOC has been built are “interoperability” and “coexistence.” The SHC adapter service has been developed to ensure interoperability and verifiability of the DIVOC’s natively issued certificates with the multiple verifier apps used in the SHC adopter countries.

## **How does the conversion utility work?**

DIVOC’s adapter issues a digital certificate, as per the SHC data model, and is presented as a signed-QR code. When a source system calls DIVOC’s SHC adapter API, the following steps are undertaken;

* DIVOC first checks within the certificate registry (using the beneficiary enrolment code, passed from the source system) to see if a certificate is present for the given beneficiary.
* If present within the certificate registry, it fetches the respective certificate and then converts the native DIVOC W3C certificate to a SHC-certificate ([**https://build.fhir.org/ig/HL7/fhir-shc-vaccination-ig/**](https://build.fhir.org/ig/HL7/fhir-shc-vaccination-ig/)) using a custom-built npm module.
* This SHC-certificate payload is then signed and the resulting JWS is used to create a QR code (using the open-source [**https://github.com/Path-Check/shc-sdk.js**](https://github.com/Path-Check/shc-sdk.js) library).
* It returns the generated QR code or the full-certificate PDF (including the signed-QR), based on type parameters.
* The source system can then allow the download of the generated SHC-QR certificate onto a beneficiary’s mobile phone or allow the export to a beneficiary’s digital wallet platform.

## **References**

### **Technical specification**

* To know more on SHC specification, click [**https://spec.smarthealth.cards/**](https://spec.smarthealth.cards/).
* You can check the SHC vaccination and testing implementation guide [**here**](https://build.fhir.org/ig/HL7/fhir-shc-vaccination-ig/).

****

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
