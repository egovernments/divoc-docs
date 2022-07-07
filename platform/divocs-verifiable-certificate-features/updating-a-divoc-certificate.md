# Updating a DIVOC Certificate

## Purpose&#x20;

The purpose of this document is to outline the features and workflow of DIVOC's “Update Certificate” service.

## **Overview**

* DIVOC provides an “update certificate” feature to help beneficiaries make changes in a certificate if any information was captured incorrectly during the beneficiary registration or vaccination process.&#x20;
* For this purpose, DIVOC provides an “_Update Certificate API_,” for a source system (e.g. a vaccination platform) to update the vaccination as well as beneficiary details in digital certificates issued by DIVOC.
* There are multiple ways of using this service. The issuing authority can enable a self-service portal, or set up a call centre, or the source system can capture the update requests directly, which can then call the Update API to facilitate the updates/corrections to the specific certificates. The key requirement here is that the “Update Certificate API” is called by the source system(s) to update an issued certificate. Using this API, the source system can update a beneficiary’s latest as well as previously issued digital certificates.

## **Update Certificate API**

As outlined earlier, DIVOC’s “Update Certificate” API is used by source systems to perform updates to already-issued certificates. You can refer to the update API specification link [**here**](https://github.com/egovernments/DIVOC/blob/main/interfaces/vaccination-api.yaml#L722)**.**

## **Sample API Payload**

```
[
  {
    "preEnrollmentCode": "987456126",
    "recipient": {
      "name": "John Doe",  
      "dob": "1987-04-21",
      "nationality": "Dutch",
      "identity": "872550100V",
      "contact": [
        "tel:1691742639"
      ]
    },
    "vaccination": {
      "name": "Covishield",
      "batch": "41202025",
      "manufacturer": "astrazeneca",
      "date": "2021-10-17T13:10",
      "effectiveStart": "2021-10-25",
      "effectiveUntil": "2022-10-24",
      "dose": 1,
      "totalDoses": 2
    },
    "vaccinator": {
      "name": "Bartjan Verduijn"
    },
    "facility": {
      "name": "MOH Gothatuwa"
    }
  }
]
```

## **What can be updated/corrected?**

1. An issued certificate’s QR code contains the two categories of information:

&#x20; \- **Personal information**, for example:

* Beneficiary name&#x20;
* Gender&#x20;
* Date of Birth

&#x20; \- **Event details**, for example:&#x20;

* Vaccine type/prophylaxis&#x20;
* Vaccine name/brand&#x20;
* Manufacturer Vaccine batch&#x20;
* Vaccination date&#x20;
* Facility ID/name&#x20;
* Country of issuance&#x20;
* Issuer&#x20;
* Dose number&#x20;
* Total dose count

2\. Any or all of the above fields can be corrected/updated by calling the Update Certificate API by a source system.&#x20;

3\. The Update Certificate API requires beneficiary ID/enrollment code and dose number as an input to fetch the right certificate that needs to be updated.&#x20;

4\. Once the certificate is fetched, the update API updates the information against the certificate ID as provided in the API payload input.&#x20;

5\. Once the certificate is updated, a new certificate is issued with a new certificate ID and updated information. The older certificate gets revoked by an automated revocation workflow using DIVOC’s “Revoke API.”&#x20;

6\. The revoked certificate is moved to the Certificate Revocation List (CRL). If the older revoked certificate is scanned by a verifier, the verification screen will show “certificate revoked.”&#x20;

7\. For update scenarios, DIVOC can also enable configuring a custom message for beneficiaries trying to verify the older corrected and revoked certificate as: “certificate revoked, please download the updated certificate from the portal.”&#x20;

8\. Updates/corrections can be made in the provisional and final certificate for any of the fields present in the QR code as per the issuing authority’s requirements and approved flow.&#x20;

9\. It is strongly recommended that an issuing authority should allow information correction/updates only after verifying the required proofs uploaded by the beneficiary.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
