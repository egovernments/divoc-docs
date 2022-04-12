# Jamaica implementation details

## Overview&#x20;

Jamaica went live with DIVOC in December 2021. DIVOC has set up the “Digital Vaccination Certificate Portal,” which also serves as the citizen portal, as well as a system admin portal for Jamaica. The vaccination data has been integrated with CommCare.

We will give you an overview of the different features and services of DIVOC that have been implemented in Jamaica and the standard used.

## Platform release version&#x20;

1.24.0-generic

## **Features and services**

* ****[**Certificate generation:**](../divocs-verifiable-certificate-features/creating-a-divoc-certificate/) **** This is in sync with the country’s COVID-19 vaccination event. Once a person gets vaccinated, information is sent to Jamaica’s vaccination system and a certificate is automatically generated via DIVOC.
* ****[**Certificate verification:**](../divocs-verifiable-certificate-features/verifying-a-divoc-certificate.md) **** The citizen portal can be used to verify the QR code-based certificates that are issued after vaccination.

![](<../.gitbook/assets/Screenshot 2022-04-04 at 2.51.40 PM.png>)

* ****[**Updating certificates:**](../divocs-verifiable-certificate-features/updating-a-divoc-certificate.md) **** DIVOC has enabled a certificate update/correction API that can be used to update or correct an issued certificate if a citizen requests it.
* ****[**Revoking certificates:**](../divocs-verifiable-certificate-features/revoking-a-divoc-certificate.md) **** This feature has been provided to Jamaica and will be implemented soon.
* SMS service: DIVOC’s certificate module has been integrated with the SMS gateway service facilitated by Jamaica. As part of this service, a notification is sent to every citizen after they get vaccinated, informing them to download their certificates from the citizen portal.
* ****[**Downloading certificates:**](../divoc-demo/citizen-portal.md#2.-for-downloading-a-certificate) **** Beneficiaries of the vaccination program can log in to the citizen portal using the 10-digit mobile number that they had used during registration and then click on “download your vaccination certificate” to view and download certificates.

![](<../.gitbook/assets/Screenshot 2022-04-04 at 2.59.42 PM.png>)

* **Print facility:** The staff or administrator at a facility will be provided with a login to use this feature to search for certificates and print them on behalf of the citizens. When a citizen walks into a facility, the staff will use the information (mobile number or date of birth) provided by him/her to search for the vaccination certificate. Once they find the certificate on the portal, the staff can download and print it.

![](<../.gitbook/assets/Screenshot 2022-04-04 at 3.01.35 PM.png>)

## Standards used&#x20;

All COVID-19 certificates are generated in the WHO-Digital Documentation of COVID-19 Certificates (DDCC) format.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
