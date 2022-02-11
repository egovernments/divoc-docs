# Revoking a DIVOC Certificate

## Purpose

This document refers to the revocation of a digital certificate issued to a person. DIVOC’s certificate revocation service will help stakeholders of a program to revoke digital certificates, according to the issuing authority’s predefined policy.

For example, during a COVID-19 vaccination campaign, the vaccination certificate issued to a person, as digitised proof of the event, can get revoked due to multiple reasons like:

* errors in the information encoded in the digital certificate.&#x20;
* wilful tampering of the digital certificate (QR or PDF output) by external entities who have gained unauthorized access to the certificate data contents.&#x20;
* or if a specific batch of vaccines is found to be faulty, among others.

The purpose of this document is to provide an overview of the certificate revocation service offered by DIVOC. It describes the steps involved in the revocation process, as well as the maintenance of the revoked certificate list for verifiers.

## **What is DIVOC’s certificate revocation service?**

### **Revocation API**

* DIVOC has enabled a “Revoke API” that can be used to revoke an issued certificate, for manual revocation use cases.&#x20;
* The API uses a “beneficiary ID/pre-enrollment code” and either the “dose number(s)” or the “all doses” flag as input parameters to search and fetch the certificate(s) that needs to be revoked from the certificate registry.&#x20;
* If the “dose number(s)” parameter is passed, it must be a sequential list of doses which includes the latest dose.&#x20;
* DIVOC stores the revoked certificate ID within a centrally-maintained “certificate revocation list” (or CRL).

### Revocation List

* DIVOC maintains a “certificate revocation list” (CRL) to store certificate IDs of the revoked certificates. The revocation list can be hosted by an issuing authority (either inside or outside its central certificate registry) or can be periodically downloaded as a file and stored by a verifier application.&#x20;
* When a revoked certificate’s QR code is scanned using the DIVOC’s online verification service, the service searches the CRL for the certificate ID to check if the certificate is a valid or revoked certificate.&#x20;
* If the certificate ID is found in the CRL of the scanned QR code, the verification screen displays the certificate as revoked.

![](<../.gitbook/assets/Screenshot 2022-02-02 at 12.20.09 PM.png>)

* Each CRL has a serial number, time, and date on which the certificate was revoked.&#x20;
* It includes the date and time when the CRL was published, and when the next update to the CRL will be published.

## How does it work?

* A revocation is triggered when the revocation API is called by the source system (e.g. a vaccination platform), on specific transactions (e.g. the correction or update of a certificate).&#x20;
* As input parameters from the source system, the Revoke API receives beneficiary ID/enrollment code and dose number(s) or the all doses flag.&#x20;
* The relevant certificate is fetched and DIVOC performs a “soft delete” of the certificate (also referred to as the “revocation” process).
* The revoked certificate’s certificate ID is then moved to the certificate revocation list.
* Certificate IDs of all revoked certificates are maintained in the CRL within the certificate registry. The revoked certificate IDs can be indexed in chronological order against the respective unique certificate ID, along with its revocation date and time.
* The certificate revocation list will be regularly updated to support the verification flow by approved domestic and international verifiers.
* If the certificate was revoked, the same information will be displayed to the third-party verifier application in real-time. On scanning, the verifier application will display the result as an “Invalid certificate.”
* DIVOC’s certificate revocation list can be configured to support both offline and online verifications flows. For instance,&#x20;

&#x20;          \- On scanning a revoked certificate, a third-party verifier application can call the APIs (i.e. fetch APIs provided by DIVOC to the country’s issuing authority) to fetch the certificate revocation list to validate the “revoked” status of the digital certificate.&#x20;

&#x20;         \- The certificate revocation list can be downloaded by the third-party verifier application (in their local system) on a periodic basis.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
