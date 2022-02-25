# DIVOC native COVID-19 certificate specification

When the “Certify API” is called by a vaccinating system, a unique QR code is generated for that specific event. This document specifies the data structure that can be used to generate a QR code-based digitally verifiable certificate for a registered health event.

## QR Payload structure

The payload structure follows the JSON Web Token (JWT) digital signature and is defined in [**RFC 7519**](https://datatracker.ietf.org/doc/html/rfc7519). The payload is transported in a DIVOC certificate. JWT includes the following:

* Header&#x20;
* Payload&#x20;
* Signature algorithm

### Header&#x20;

This contains the information about the certificate, which is based on the [**W3C verifiable credentials data model**](https://www.w3.org/TR/vc-data-model/). The header also indicates the type of certificate being issued.&#x20;

### Payload&#x20;

This is divided into several parts:&#x20;

* The first part contains the details of who is issuing the certificate along with the timestamp.&#x20;
* The second part contains the details of the beneficiary to whom the certificate has been issued.&#x20;
* The final part contains details on the event for which the certificate has been generated. The event part has details of the health event (such as vaccination) along with a timestamp, which includes information on the type of vaccine, dose details, and location of the vaccination.

### Signature algorithm&#x20;

DIVOC is capable of self-generating a public-private key pair. It also supports a signing configuration where the country has onboarded a CA (certificate authority) responsible for generating the keys. In the latter case, DIVOC will use the private key issued by the CA and sign the QR code.

* The DIVOC certificate is flexible and multiple signing algorithms can be used.&#x20;
* Self-generated keys or the keys from a country’s PKI service provider can also be used. DIVOC currently uses two default signature algorithms:&#x20;

&#x20;              1\. PS256 - Using "crit" with "b64"&#x20;

&#x20;                 ([**https://w3c-ccg.github.io/security-vocab/#RsaSignature2018**](https://w3c-ccg.github.io/security-vocab/#RsaSignature2018))

&#x20;              2\. ES256&#x20;

&#x20;                  ([**https://w3c-ccg.github.io/security-vocab/#EcdsaSecp256k1Signature2019**](https://w3c-ccg.github.io/security-vocab/#EcdsaSecp256k1Signature2019))

* Click [**here**](https://github.com/egovernments/DIVOC/blob/f3c524ff0e8e9a2f09193a37758a67e9b7198c31/public\_app/src/utils/credentials.json) to see the various versions of the algorithm.&#x20;
* The public key along with the method of signing will be provided to verifiers to authenticate certificates.&#x20;
* Based on the algorithm that is being used for certificate generation, the certificate can be verified by the verifier.

### Sample Payload

```
{
   "@context":[
      "https://www.w3.org/2018/credentials/v1",
      "https://cowin.gov.in/credentials/vaccination/v1" 
   ],
   "type":[
      "VerifiableCredential",
      "ProofOfVaccinationCredential"
   ],
   "credentialSubject":{
      "type":"Person",
      "id":"19882120590",
      "refId":"77889950",
      "name":"Juan Dela Cruz ",
      "gender":"Female",
      "age":"33",
      “dob”:””,
      "nationality":"India",
      "address":{
         "streetAddress":"114/1/15,Horahena Road, Kottawa",
         "streetAddress2":"",
         "district":"colombo",
         "city":"",
         "addressRegion":"Western",
         "addressCountry":"IN",
         "postalCode":"121212"
      }
   },
   "issuer":"https://cowin.gov.in/",
   "issuanceDate":"2021-06-28T07:21:39.684Z",
   "evidence":[
      {
         "id":"https://cowin.gov.in/vaccine/448086902",  
         "feedbackUrl":"https://cowin.gov.in/?448086902",
         "infoUrl":"https://cowin.gov.in/?448086902", 
         "certificateId":"448086902",
         "type":[
            "Vaccination"
         ],
         "batch":"batch-01",
         "vaccine":"Pfizer",
         "manufacturer":"US",
         "date":"2021-06-28T05:30:28.187Z",
         "effectiveStart":"2021-04-21",
         "effectiveUntil":"2022-04-21",
         "dose":1,
         "totalDoses":2,
         "verifier":{
            "name":"ss"
         },
         "facility":{
            "name":"MOH Gothatuwa",
            "address":{
               "streetAddress":"df",
               "streetAddress2":"",
               "district":"wew",
               "city":"",
               "addressRegion":"w",
               "addressCountry":"IN",
               "postalCode":"121212"
            }
         }
      }
   ],
   "nonTransferable":"true",
   "proof":{
   "type":"RsaSignature2018",
      "created":"2021-06-28T07:21:39Z",
      "verificationMethod":"did:india",
      "proofPurpose":"assertionMethod",
      "jws":"eyJhbGciOiJQUzI1NiIsImI################4v_Gq6tIkDfhQQ"
   }
}
```

* Click [**here**](../what-information-goes-into-a-qr-code.md) **** to know more about what data set goes inside the QR code.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
