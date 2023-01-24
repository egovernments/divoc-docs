# DIVOC 3.1 Release Features

## Version release date

November 21, 2022

## Release summary&#x20;

With this release, the DIVOC platform can now generate different types of verifiable credentials. It is no longer restricted to vaccination-specific verifiable credentials.

## Terminology

A list of the common terms used in this document:

* [**Verifiable credentials (VCs)**](https://www.w3.org/TR/vc-data-model/) **** represent information found in physical credentials, such as birth registration and driving license, as well as objects that have no physical equivalent, such as ownership of a bank account. VCs are typically QR codes whose information is being signed and can only be modified by the issuer making it a tamper proof QR code. The QR codes can be read and verified by  the verifiers using the public key issued by the issuer and by using the libraries/algorithms used by the issuer system. When a digital document (for example, a lab test report) has a normal QR code, anyone can modify its value and generate new QR code and then replace it with another QR code with different information. Whereas the information in a verifiable QR code cannot be replaced as the original data or information cannot be changed without a “private key.”
* Issuer: Refers to an issuing authority who can issue claims about a particular entity or individual that can be validated. An issuer gathers the information that needs to be contained in the VC from the entities and sends it across to DIVOC through tenant software. Example: Medical Councils.
* Tenant: Refers to any source system of issuers linked to the DIVOC platform to issue VCs. Examples: Council Software, University software, etc.
* Source systems: The tenant software that interacts with the DIVOC platform to issue VCs.
* Schema: A schema is essentially a template that tells the issuer the content, type, and description required for an attribute that needs to be part of the VC.
* For example, a schema can be as follows with multiple rows for other parameters:

| Field name      | Type         | Description                                                     | Mandatory |
| --------------- | ------------ | --------------------------------------------------------------- | --------- |
| Registration No | Alphanumeric | This is the registration number issued to a health professional | Yes       |

* Beneficiary: Refers to the holder of the VC. Examples: Doctors, students, etc.
* S-RC - Sunbird R C: This is a set of configurable, extendable, modular building blocks for learning and human development designed for scale and open-sourced under an MIT license. (Definition courtesy: [**Sunbird**](https://sunbird.org/about-us)**).**
* UI: User interface.

## New Features

| Feature             | Description                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Verification portal | <p>This will enable verifiers to check the authenticity and validity of VCs issued using the DIVOC system from different issuers/tenant systems by scanning the QR codes through an interface. The verification will identify certificate as:  </p><ol><li>Valid certificate </li><li>Invalid certificate </li><li>Suspended certificate </li><li>Revoked certificate</li></ol> |

## **Enhancements from the previous platform release**

| Enhancement                    | Description                                                                                                                                                                                       |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bug fixes and package upgrades | This includes minor changes in certification and management services to support upgraded Sunbird-registry and Sunbird-signer services, which added support for ECDSA keys in the signing process. |

## **Upcoming features**

| Enhancement                     | Description                                                                                                                     |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| UI for tenant onboarding portal | An interface through which source system administrators can log in to the DIVOC platform and connect it with the source system. |
| UI for multiple schema creation | An interface through which source system administrators can create and manage different schemas required for issuing VCs.       |

****

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
