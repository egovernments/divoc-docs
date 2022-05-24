# DIVOC’s certificate generation service: How does it work?

This section covers the following:

* Certificate generation process&#x20;
* Certify APIs
* API structure

## Certificate generation process

It involves the following steps:&#x20;

* Recording of a health event against a unique beneficiary, either in the source eHealth system (or in the DIVOC vaccination module, if used by a country, for their vaccination campaign). This results in the creation of the dataset for the specific event.&#x20;
* The event records all transactions associated with it (e.g. beneficiary demographics, vaccinator/facility details, certificate metadata, and timestamp, among others).&#x20;
* Marking the completion of the "event" in the system triggers a DIVOC certificate generation API (or “Certify” API), with the event data populated as per the defined API structure.&#x20;
* DIVOC’s certificate module receives the event data.&#x20;
* A digital certificate, encompassing both a QR code and a human readable document (e.g. PDF) is then issued, which holds the event data for the beneficiary, along with a unique certificate ID.&#x20;
* The QR code is signed with the issuing authority (e.g. national/provincial health agency) private key.&#x20;
* A summary of the health event is then used to populate the “human readable” part of the digital certificate.

![](<../../.gitbook/assets/Screenshot 2022-01-27 at 10.31.18 AM.png>)

### Output

The generated output has two parts:&#x20;

* It has a human-readable document (e.g. the PDF) and the machine-readable QR (the signed QR).&#x20;
* The digital certificate can be presented back to the source system in either of the ways (i.e. either just the signed QR as an image file, or the entire PDF output with the signed QR).

### Sample

A sample DIVOC certificate output is further illustrated in the image below:

![](<../../.gitbook/assets/Screenshot 2022-01-27 at 10.34.28 AM.png>)

## Certify APIs

The DIVOC certificate generation service provides a “Certify” API for other eHealth systems, to generate digital certificates for specific events. Currently, DIVOC provides two certify APIs for a “COVID-19 vaccination certificate” and “COVID-19 test result certificate” respectively.

| API type                         | API reference link                                                                                                                                                                   |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| “Certify” for vaccination events | [**https://github.com/egovernments/DIVOC/blob/main/interfaces/vaccination-api.yaml#L722**](https://github.com/egovernments/DIVOC/blob/main/interfaces/vaccination-api.yaml#L722)**** |
| “Certify” for test result events | [**https://github.com/egovernments/DIVOC/blob/main/interfaces/vaccination-api.yaml#L877**](https://github.com/egovernments/DIVOC/blob/main/interfaces/vaccination-api.yaml#L877)**** |

## API structure

The API structure for the Certify API includes the following:

1. **Recipient information:** This section contains information about the beneficiary of the specific health event (e.g. COVID-19 vaccination or test event).&#x20;
2. **Vaccination event information:** This includes details about the vaccination event such as name, batch, and vaccination date, as well as the vaccinator.&#x20;
3. **Issuer information:** It contains information about the issuing authority.&#x20;
4. **Certificate information:** It includes details such as certificate ID and expiry date, among others.&#x20;
5. **Meta:** This part is used to populate related information about a previous event in the human-readable PDF twin of the digital certificate that can be used by the verifier for cross-reference. It contains additional information, which is not part of the current QR code (the QR code only contains information about the current event), such as the number of past doses taken. For example, If a QR code is generated for the final dose certificate, the QR code will contain all information about the final dose. If a country wants to show information about the previous dose, that can be populated from meta in the certificate PDF.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
