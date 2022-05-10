# Issuing COVID-19 Vaccination Certificates in India

The Government of India launched the COVID-19 vaccination program in January 2021. The roll-out of the Co-WIN application was key to this. While the cloud-based platform covered all the major modules that a vaccination program of this scale should have, it lacked the digital credentialing feature that was critical to open up travel and economy amid the COVID-19 pandemic. DIVOC was integrated with Co-WIN in January 2021, making India the first country where the digital verifiable credentialing was implemented. Over 1.9 billion vaccination certificates have been issued in India so far.

## Platform release version&#x20;

Since India was the first country to implement DIVOC, a component-wise release was done as there was no generic version available back then. Hence, the release versions are component-specific:

| Components                                                                               | Release Version |
| ---------------------------------------------------------------------------------------- | --------------- |
| Certificate generation services: dockerhub/divoc-certification-ack                       | 1.0.16          |
| Certificate generation services: dockerhub/certificate\_processor                        | 1.0.16          |
| Certificate generation services: dockerhub/certificate\_signer                           | 1.0.22          |
| Certificate generation services:  dockerhub/vaccination\_api                             | 1.0.27          |
| Certificate generation services - Commonly-used component: dockerhub/registry            | 1.0.19          |
| Certificate generation services - Commonly-used component: dockerhub/caching-dash-server | 1.0.20          |
| Verification component: dockerhub/verification                                           | 1.0.29          |
| Certificate reconciliation services: dockerhub/reconciliation                            | 1.0.3           |
| Fetch certificate services: dockerhub/digilocker\_support\_api                           | 1.0.59          |
| Fetch certificate services: dockerhub/registry                                           | 1.0.19          |
| Dashboard: dockerhub/analytics\_feed                                                     | 1.0.17          |

## Features and services

[**Certificate generation:**](../divocs-verifiable-certificate-features/creating-a-divoc-certificate/) **** A certificate is generated in real-time every time a person’s vaccination record is created in Co-WIN. Citizens get the latest dose certificate, which could be provisional, final, or the precaution dose. Two types of certificates are issued: domestic (age is mandatory) and international travel certificates (date of birth is mandatory). Further, DIVOC certificates (domestic) can be generated in 22 languages in India.

****[**Certificate download:**](../divoc-demo/citizen-portal.md#2.-for-downloading-a-certificate) **** Besides Co-WIN, DIVOC’s certificate module has been integrated with **** [**Arogya Setu**](https://www.aarogyasetu.gov.in)**,** [**Umang**](https://web.umang.gov.in/landing/)**,** and [**Digilocker**](https://www.digilocker.gov.in)**,** so that citizens can download their certificates after vaccination from any of these portals/apps by using their registered mobile number.&#x20;

![](<../.gitbook/assets/Screenshot 2022-04-19 at 2.03.01 PM.png>)

****[**Certificate verification:**](../divocs-verifiable-certificate-features/verifying-a-divoc-certificate.md) DIVOC’s integration with CoWIN enables verification of the QR code-based vaccination certificates [**online**](https://verify.cowin.gov.in) by using DIVOC’s verification utility embedded within Co-WIN.

![](<../.gitbook/assets/Screenshot 2022-04-19 at 2.07.18 PM.png>)

****[**Updating certificates:**](../divocs-verifiable-certificate-features/updating-a-divoc-certificate.md) This feature can be used by citizens if the name, age, gender, date of vaccination, or other details on their vaccination certificate are incorrect.

****[**Revoking certificates:**](../divocs-verifiable-certificate-features/revoking-a-divoc-certificate.md) This feature is also used in India.

****[**Analytics:**](../divoc-demo/analytics.md) **** DIVOC has set up a [**dashboard**](https://stats.cowin.gov.in/public/dashboards/HT9vhThnsXTQcuLUrFprMz97moerYPnRqtf7WRPn) **** for India, which gives a snapshot of the total number of certificates issued, and accessed.

![Note: These are April 19, 2022, numbers](<../.gitbook/assets/Screenshot 2022-04-19 at 2.13.17 PM.png>)

## Standards used

* The international certificates issued in India for citizens traveling abroad are based on the     [**WHO-Digital Documentation of COVID-19 Certificates (DDCC)**](https://www.who.int/publications/i/item/WHO-2019-nCoV-Digital\_certificates-vaccination-2021.1) data specification.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
