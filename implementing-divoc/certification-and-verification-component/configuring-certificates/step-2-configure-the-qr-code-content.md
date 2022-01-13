# Step 2: Configure the QR code content

The template for the QR code generation is provided [**here**](https://github.com/egovernments/DIVOC/blob/main/vaccination-context/vaccination-context.js) under vaccination-context. The QR code structure must match the vaccination-context. Any updates made in the QR code content must reflect in the vaccination-context.js file.

**Steps:**

a. Open the file [**main.js**](https://github.com/egovernments/DIVOC/blob/main/backend/certificate\_signer/main.js).

b. Go to the function transformW3 and add the fields according to your requirement. This function will read the data received from the certificate generation API call and convert it into QR code Json format.

```markup
function transformW3(cert, certificateId) {
  const certificateType = R.pathOr('', ['meta', 'certificateType'], cert);
  const namespace = certificateType === CERTIFICATE_TYPE_V3 ? CERTIFICATE_NAMESPACE_V2 : CERTIFICATE_NAMESPACE;
  const recipientIdentifier = R.pathOr('', ['recipient', 'identity'], cert);
  const preEnrollmentCode = R.pathOr('', ['preEnrollmentCode'], cert);
  const recipientName = R.pathOr('', ['recipient', 'name'], cert);
  const recipientGender = R.pathOr('', ['recipient', 'gender'], cert);
  const recipientNationality = R.pathOr('', ['recipient', 'nationality'], cert);
  const recipientParentName = R.pathOr('', ['recipient', 'parentName'], cert);
```

c. Add the newly-added field to the data variable

```
let data = {
    namespace, recipientIdentifier, preEnrollmentCode, recipientName, recipientGender, recipientDob, recipientAge, recipientNationality, recipientParentName, recipientAddressLine1, recipientAddressLine2, recipientAddressDistrict, recipientAddressCity, recipientAddressRegion, recipientAddressCountry, recipientAddressPostalCode,
    issuer, issuanceDate, evidenceId, InfoUrl, feedbackUrl,
    certificateId, batch, vaccine, icd11Code,  prophylaxis, manufacturer, vaccinationDate, effectiveStart, effectiveUntil, dose, totalDoses,
    verifierName,
    facilityName, facilityAddressLine1, facilityAddressLine2, facilityAddressDistrict, facilityAddressCity, facilityAddressRegion, facilityAddressCountry, facilityAddressPostalCode
  };
```

**Note:**&#x20;

Certain constant values are also listed in **** the **** [**main.js**](https://github.com/egovernments/DIVOC/blob/main/backend/certificate\_signer/main.js)**.** If you want to update any of the constant values such as “certificate controller,” please refer to the **** [**DockerFile**](https://github.com/egovernments/DIVOC/blob/main/backend/certificate\_signer/Dockerfile).



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
