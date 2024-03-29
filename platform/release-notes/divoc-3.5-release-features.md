# DIVOC 3.5 Release Features

## Version release date

January 24, 2023

## Release summary

With this release, the DIVOC platform provides a user interface (UI) for tenants to log into the DIVOC platform to create and manage different tenants and schemas required for issuing verifiable credentials (VCs).

## Terminology

A list of the common terms used in this document:

* [**Verifiable credentials (VCs)**](https://www.w3.org/TR/vc-data-model/) **** represent information found in physical credentials, such as birth registration and driving license, as well as objects that have no physical equivalent, such as ownership of a bank account. VCs are typically QR codes whose information is being signed and can only be modified by the issuer making it a tamper-proof QR code. The QR codes can be read and verified by the verifiers using the public key issued by the issuer and by using the libraries/algorithms used by the issuer system. When a digital document (for example, a lab test report) has a normal QR code, anyone can modify its value and generate a new QR code and then replace it with another QR code with different information. Whereas the information in a verifiable QR code cannot be replaced as the original data or information cannot be changed without a “private key.”
* Issuer: Refers to an issuing authority who can issue claims about a particular entity or individual that can be validated. An issuer gathers the information that needs to be contained in the VC from the entities and sends it across to DIVOC through tenant software. Example: Medical Councils.
* Tenant: Refers to any source system of issuers linked to the DIVOC platform to issue VCs. Examples: Council Software, University software, etc.
* Source systems: The tenant software that interacts with the DIVOC platform to issue VCs.
* Schema: A schema is essentially a template that tells the issuer the content, type, and description required for an attribute that needs to be part of the VC.

## New Features

| Enhancement                                      | Description                                                                                                                                                                                                                                                                       |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UI for tenant onboarding portal                  | An interface through which source system administrators can log into the DIVOC platform and connect it with the source system.                                                                                                                                                    |
| UI for credentials management                    | A UI-based interface through which tenant administrators can regenerate their API keys to connect to the DIVOC platform and generate access tokens.                                                                                                                               |
| UI for multiple schema creation and modification | An interface through which tenant administrators can create and manage different schemas required for issuing VCs. This provides functionality to ingest the schema from a JSON or use the user interface to add fields to the schema, as well as set various attributes to them. |
| UI for schema creation preview                   | Test and preview the certificate being generated before the schema could be published.                                                                                                                                                                                            |
| UI for managing certificate templates            | Add and modify templates for certificates generated by the DIVOC platform.                                                                                                                                                                                                        |

## Enhancements from the previous platform release

| Enhancement            | Description                                                                                                                                                      |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bug fixes and upgrades | This includes minor changes in certification and management services to support the upgraded Sunbird registry for updating schema and some UI-specific services. |



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
