# Roadmap

The DIVOC roadmap is a snapshot of our upcoming features and tools.

### Quarter 1+Quarter 2: April-September 2022

| Feature                                                                  | Description                                                                                                                                                                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Manage multiple tenants                                                  | Services to manage multiple tenants and their respective schema.                                                                                                                                                         |
| Create verifiable credentials (VCs) from multiple issuers                | Ability to create VCs with different schemas for one tenant and to create VCs from multiple issuers.                                                                                                                     |
| Ability to update schema                                                 | Ability to make changes or updates to available schemas.                                                                                                                                                                 |
| Service to generate and send only QR code (SVG) with provided dimensions | The tenant/issuer system can fetch images of QR codes in provided dimensions. The image can be shared with the beneficiary directly or can be embedded in the certificate template designed by the issuer/tenant system. |
| Services to update certificate                                           | Capability to update/modify already generated certificates.                                                                                                                                                              |
| Revocation and suspension                                                | Capability to revoke or suspense already issued certificates upon expiry, issuance of a newer version, or violation of terms and conditions.                                                                             |
| Notification services                                                    | Capability to notify beneficiaries on the generation of certificates.                                                                                                                                                    |
| Enabling multi-lingual certificate                                       | Functionality to manage certificate templates in multiple languages and generate certificates based on selected templates.                                                                                               |

### Quarter 3: October-December 2022

| Feature                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Common verification portal | <p>A common verifier portal for verifying VCs created by multiple schemas and from multiple issuers. The portal will have a UI that will be accessible to the public, or those with credentials to access them. For example, a doctor with a VC for council registration created by the DIVOC platform submits the same to an employer (a hospital). The hospital can then go to the common verification portal URL and verify the VC. </p><p></p><p>The verification portal can verify the following:  </p><p>1. Authenticity (If the certificate has been tampered with). </p><p>2. Status (The certificate is revoked/suspended/is valid/is not valid).</p> |
| Tenant onboarding UI       | <p>A UI through which the source system admin can: 1. Log in to the DIVOC platform with the credentials received. </p><p>2. Reset the password if not accessible. </p><p>3. Generate tokens to connect the source system and DIVOC platform.</p>                                                                                                                                                                                                                                                                                                                                                                                                               |
| Tenant creates schema UI   | A UI through which the source system admin can define and create schemas for different provider types, and also test and publish the schemas.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

### Other features in consideration

* Verification app
* Telemetry capability for the platform
* Capability to issue multiple key pairs for different tenants
* Building trust network for key management
* UI for proof of concept of the VC capability



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
