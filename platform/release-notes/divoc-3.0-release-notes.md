# DIVOC 3.0 Release Notes

## Version release date

* September 21, 2022

## Release summary

With this release, the DIVOC platform can now generate different types of verifiable credentials. It is no longer restricted to vaccination-specific verifiable credentials.

#### A list of the common terms used in this document:

* ****[**Verifiable credentials (VCs)**](https://www.w3.org/TR/vc-data-model/) **** represent information found in physical credentials, such as birth registration and driving license, as well as objects that have no physical equivalent, such as ownership of a bank account. VCs are typically QR codes whose information can only be unlocked by verifiers (for example, a medical council registration certificate with a QR code). When a digital document (for example, a lab test report) has a normal QR code, anyone can read all the information inside the QR by using widely available software on the internet. Such software can read the QR code and then replace it with another QR code with different information. Whereas the information in a verifiable QR code cannot be replaced as the original data or information cannot be changed without a “private key.”
* Issuer: Refers to an issuing authority who can issue claims about a particular entity or individual that can be validated. An issuer gathers the information that needs to be contained in the VC from the entities and sends it across to DIVOC through tenant software. Example: Medical Councils.
* Tenant: Refers to any source system of issuers linked to the DIVOC platform to issue VCs. Examples: Council Software, University software, etc.
* Source systems: The tenant software that interacts with the DIVOC platform to issue VCs.
* Schema: A schema is essentially a template that tells the issuer the content, type, and description required for an attribute that needs to be part of the VC. For example, a schema can be as follows with multiple rows for other parameters:

| Field name       | Type         | Description                                                     | Mandatory |
| ---------------- | ------------ | --------------------------------------------------------------- | --------- |
| Registration no. | Alphanumeric | This is the registration number issued to a health professional | Yes       |

* Beneficiary: Refers to the holder of the VC. Examples: Doctors, students, etc.
* S-RC - Sunbird R C: This is a [**set of configurable, extendable, modular building blocks**](https://sunbird.org/about-us) for learning and human development designed for scale and open-sourced under an MIT license. (Definition courtesy: Sunbird).
* UI: User interface

## New features

| Feature                                                                  | Description                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| APIs for tenant and schemas                                              | Multiple tenants can now create and manage schemas through the platform.                                                                                                                                                                                                                                                     |
| APIs for tenant and schemas                                              | A single tenant can create multiple schemas required for issuing VCs through the DIVOC platform.                                                                                                                                                                                                                             |
| Ability to update the schema                                             | This will give you the capability to update schemas that are already created.                                                                                                                                                                                                                                                |
| Service to generate and send only QR code (SVG) with provided dimensions | Issuers can fetch QR codes through the DIVOC platform and this can be shared with the beneficiary directly or can be embedded on the certificate template.                                                                                                                                                                   |
| Services to update a certificate                                         | We have added the capability to [**update/modify**](../divocs-verifiable-certificate-features/updating-a-divoc-certificate.md) **** content on already generated certificates.                                                                                                                                               |
| APIs for revocation and suspension                                       | An issued certificate may need to be [**revoked/suspended**](../divocs-verifiable-certificate-features/revoking-a-divoc-certificate.md) due to validity expiry, issuance of a new certificate, or violation of terms and conditions. With this release, issuers can revoke and suspend certificates that are already issued. |
| Notification services                                                    | The beneficiaries (holders of the VC) will receive an SMS when the certificates are generated.                                                                                                                                                                                                                               |
| Enabling multi-lingual certificate                                       | We have added the capability to create and issue certificates in multiple languages.                                                                                                                                                                                                                                         |

## **Enhancements from previous platform release**

| Feature                                                  | Description                                                                                                                 |
| -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Add support in DIVOC to use S-RC in async mode           | DIVOC platform has been updated for the services to work in async mode to avoid any data loss during high transaction load. |
| Modifications in the response codes for error messages\* | Error codes have been defined and included in the response along with their corresponding error messages.                   |
| Modify Keycloak services for tenant management services  | Configured Keycloak services to support the creation of multiple tenants.                                                   |

## **Upcoming features/enhancement**

| Feature/enhancement                    | Description                                                                                                                                           |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Verification portal                    | This will enable verifiers to check the authenticity and validity of VCs issued from different issuers by scanning the QR codes through an interface. |
| UI for tenant onboarding portal        | An interface through which source system administrators can log in to the DIVOC platform and connect it with the source system.                       |
| UI for tenant multiple schema creation | An interface through which source system admins can create and manage different schemas required for the issuance of VCs.                             |

### Annexure&#x20;

\*Error codes and their corresponding responses

| Error code | Message                                                                                 |
| ---------- | --------------------------------------------------------------------------------------- |
| 400        | Invalid input provided.                                                                 |
| 401        | Unauthorised (in case the token has expired or is invalid).                             |
| 403        | Forbidden (if any required headers/auth header is not available).                       |
| 404        | Not found (in case of any unavailable resources).                                       |
| 406        | Specific for failed verification (during scanning of the QR code).                      |
| 500        | Any other internal server error (usually in case the error is not from the list above). |
| 502        | Thrown by the gateway when a service is not reachable.                                  |

****

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
