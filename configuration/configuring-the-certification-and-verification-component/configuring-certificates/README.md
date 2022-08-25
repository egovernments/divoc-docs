# Configuring certificates

## Overview

This document will help an implementer configure a certificate (template and QR code) for a health event such as vaccination. This section includes configuring:

* [Generating Signed Key Pairs](../generating-signed-key-pairs.md)
* [Certificate generation request](step-1-create-a-certification-generation-request.md)&#x20;
* [QR code section](step-2-configure-the-qr-code-content.md)&#x20;
* [Certificate template](step-3-configure-the-certificate-template.md)

## API&#x20;

The DIVOC platform provides API services for generating digitally verifiable QR code-based vaccination certificates. The API for certificate generation has 6 sections:

1. **PreEnrollmentCode:** This section is linked to the “dose” in the vaccination section to uniquely identify the event. For example, beneficiary registration number (R101) and dose number (1) as (R101-1) will be used to identify the first dose event uniquely. Similarly, beneficiary registration number (R101) and dose number (2) as (R101-2) will be used to identify the second dose event uniquely.
2. **Recipient:** It contains information about the beneficiary.
3. **Vaccination:** It contains details about the vaccination event such as name, batch, and vaccination date.
4. **Vaccinator:** It contains details about the vaccinator.
5. **Facility:** It contains details about the facility where beneficiaries will get vaccinated.
6. **Meta:** It contains additional information, which is not part of the QR code, such as the number of past doses taken.&#x20;

## Sample for default certificate generation request

* You can refer to the API service call with sample data below:

```
[
    {
        "preEnrollmentCode": "62",
        "recipient": {
            "name": "Sam",
            "uhid": "abc2232",
            "dob": "1990-09-14",
            "age": "31",
            "gender": "Male",
            "nationality": "India",
            "identity": "did:in.gov.uidai.aadhaar:11112222334",
            "contact": [
                "tel:1111111313"
            ],
            "address": {
                "addressLine1": "123, Koramangala",
                "addressLine2": "",
                "district": "Bengaluru South",
                "state": "bihar",
                "pincode": "560033"
            }
        },
        "vaccination": {
            "name": "covaxin",
            "batch": "AB348FS",
            "manufacturer": "Bharat Biotech",
            "date": "2021-07-12T19:21:19.646Z",
            "effectiveStart": "2021-07-12",
            "effectiveUntil": "2021-08-12",
            "dose": 2,
            "totalDoses": 2
        },
        "vaccinator": {
            "name": "Sooraj Singh"
        },
        "facility": {
            "name": "ABCD Medical Center",
            "address": {
                "addressLine1": "123, Koramangala",
                "addressLine2": "",
                "district": "Bengaluru South",
                "state": "Karnataka",
                "pincode": "560033"
            }
        },
        "programId": "6ce74c0f-b1b5-4b20-9fa2-084acbbd857a",
        "meta": { //Meta section stored as an Object and it can contain information in    Key value pair
        }
    }
]\
```

* Refer to the /v3/certify service [**here**](https://raw.githubusercontent.com/egovernments/DIVOC/india/interfaces/vaccination-api.yaml) for details.&#x20;
* Click [**here**](../../../platform/divocs-verifiable-certificate-features/what-information-goes-into-a-qr-code.md) if you want to understand the mandatory and non-mandatory information that should be there in a vaccination certificate, according to global standards.

## Key Functionalities&#x20;

* Generate configured QR code&#x20;
* Generate configured certificate template

## Prerequisite: Get details on API request and field validations

a. Please refer to the existing service details in the ‘certification’ section (/v3/certify): [**https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#../../india/interfaces/vaccination-api.yaml**](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#../../india/interfaces/vaccination-api.yaml)****

b. The detailed field validations are mentioned here: [**https://github.com/egovernments/DIVOC/blob/4076e69cf152fd76dafa8a0565777895f55b1245/interfaces/vaccination-api.yaml**](https://github.com/egovernments/DIVOC/blob/4076e69cf152fd76dafa8a0565777895f55b1245/interfaces/vaccination-api.yaml) ****&#x20;

```
// /v3/certify:
    post:
      tags:
        - certification
      summary: Certify the one or more vaccination
      description: >-
        Certification happens asynchronously, this requires vaccinator
        authorization and vaccinator should be trained for the vaccination that
        is being certified. The payload for this API is compliant with DDCC core
        data set prescribed by WHO
      operationId: certifyV3
      parameters:
        - in: body
          name: body
          required: true
          schema:
            type: array
            items:
              $ref: '#/definitions/CertificationRequestV2' //Refer Line 722 in same file 
      responses:
        '200':
          description: OK
        '400':
          description: Invalid input
          schema:
            $ref: '#/definitions/Error'
```

## Making the changes

Click the following to see how you can make the changes:

1. ****[**Create a certification generation request**](step-1-create-a-certification-generation-request.md)****
2. ****[**Update the QR code content**](step-2-configure-the-qr-code-content.md)****
3. ****[**Update the certificate template**](step-3-configure-the-certificate-template.md)****



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
