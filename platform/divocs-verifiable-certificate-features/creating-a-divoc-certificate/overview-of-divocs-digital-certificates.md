# Overview of DIVOC’s digital certificates

Using the DIVOC certificate generation service, a country can issue a QR code-based digitally verifiable certificate, which serves as proof of the health event, such as the COVID-19 vaccination. It involves an issuer (for example, a government department), a holder (for example, the citizen of a country), and a verifier (for example, security personnel at the airport).

### Globally accepted W3C-Verifiable Credential Data Model

* All DIVOC issued digital certificates are based on the globally accepted W3C-Verifiable Credential Data Model 1.0.&#x20;
* DIVOC uses this [**data model**](https://www.w3.org/TR/vc-data-model/) for encoding the event data into the digital certificate’s QR code. DIVOC also uses a PKI mechanism to cryptographically sign all QR codes in the issued digital certificates.&#x20;
* Popular cryptographic signing algorithms (like RSA, EDDSA) are adopted in the DIVOC certificate QR signing process.

![Credit: Figure taken from W3C Verifiable Credentials Data Model v1.1](<../../../.gitbook/assets/Screenshot 2022-01-27 at 9.50.34 AM.png>)

### Key roles of a verifiable credential

**A. Holder:** Someone who possesses one or more verifiable credentials as a proof of an event/identified use case and is responsible for generating presentations from them. In DIVOC’s vaccination use case, it is the vaccine recipient or beneficiary.

**B. Issuer:** Reefers to a legal entity that asserts claims about the holder or subject about a verifiable event or an identified use case by issuing a verifiable credential to a holder. Issuers may include central/state governments, authorities, corporations, etc. For instance, in the COVID 19 vaccine scenario, the issuer could be the issuing country or legal authorities.&#x20;

**C. Subject:** An entity about which the verifiable claim is made by the issuer, for example, beneficiary or vaccine dose recipient.&#x20;

**D. Verifier:** An entity who is responsible for verifying an issued credential. In the COVID-19 travel scenario, verifiers are the arrival country authorities that require a verifiable COVID-19 vaccine proof for allowing access to services and border entries.&#x20;

**E. Verifiable data registry:** This refers to a role that a system may perform by mediating the creation and verification of identifiers, keys, and other relevant data, such as verifiable credential schemas, revocation registries, issuer public keys, and so on, which may be required to use verifiable credentials.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
