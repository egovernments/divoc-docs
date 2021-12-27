# Updating Certificates

## Overview

This document will help an implementer make changes to the certificate (template and QR code). This section will cover the steps to update a certificate by configuring:

1. Certificate generation request&#x20;
2. QR code section&#x20;
3. Certificate template

## API&#x20;

The DIVOC platform provides API services for generating digitally verifiable QR code-based vaccination certificates. The API for certificate generation has 6 sections:

1. **PreEnrollmentCode:** This section is linked to the “dose” in the vaccination section to uniquely identify the event. For example, beneficiary registration number (R101) and dose number (1) as (R101-1) will be used to identify the first dose event uniquely. Similarly, beneficiary registration number (R101) and dose number (2) as (R101-2) will be used to identify the second dose event uniquely.
2. Recipient: It contains information about the beneficiary.
3. Vaccination: It contains details about the vaccination event such as name, batch, and vaccination date.
4. **Vaccinator:** It contains details about the vaccinator.
5. **Facility:** It contains details about the facility where beneficiaries will get vaccinated.
6. **Meta:** It contains additional information, which is not part of the QR code, such as the number of past doses taken.&#x20;

## Sample for default certificate generation request

* You can refer to the API service call with sample data below:

![](<../../../.gitbook/assets/Screenshot 2021-12-27 at 8.54.13 AM.png>)

* Refer /v3/certify service [**here**](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#/../..) for details.&#x20;
* Click [**here**](https://docs.google.com/document/d/13EnZYs-CdKYh3GSjyAQJ7jecAdch3HBqAZ0VDokhKE8/edit#heading=h.qlnvn9e0z4em) if you want to understand the mandatory and non-mandatory information that should be there in a vaccination certificate, according to global standards.

## Key Functionalities&#x20;

* Generate updated QR code&#x20;
* Generate updated certificate template

## Prerequisite: Get details on API request and field validations

a. Please refer to the existing service details in the ‘certification’ section (/v3/certify): [**https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#../../india/interfaces/vaccination-api.yaml**](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#../../india/interfaces/vaccination-api.yaml)****

b. The detailed field validations are mentioned here: [**https://github.com/egovernments/DIVOC/blob/4076e69cf152fd76dafa8a0565777895f55b1245/interfaces/vaccination-api.yaml**](https://github.com/egovernments/DIVOC/blob/4076e69cf152fd76dafa8a0565777895f55b1245/interfaces/vaccination-api.yaml) **(Line 148: /v3/certify)**

![](<../../../.gitbook/assets/Screenshot 2021-12-27 at 9.01.00 AM.png>)

## Making the changes

Click the following to see how you can make the changes:

1. ****[**Create a certification generation request**](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/BzDN8TNEi1Pzc9yUiD8a/c/gLYIzqlPeSHxsbFeRaQW/implementers-guide/certification-and-verification-component/updating-certificates/step-1-create-a-certification-generation-request)****
2. **Update the QR code content**
3. **Update the certificate template**











