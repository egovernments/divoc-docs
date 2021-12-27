# Step 3: Update the certificate template

Each country will have a separate certificate template with country-specific branding, and language.

**Steps:**

a. The DIVOC certificate template has been designed in the HTML format. To update the HTML**-**based certificate template according to your country’s requirement, open [**certificate\_template.html**](https://github.com/egovernments/DIVOC/blob/main/backend/certificate\_api/configs/templates/certificate\_template.html) and map the dynamic fields in the certificate template.

```
<tr>
        <td><span class="d-flex pt-1 pb-1 font-bold">Beneficiary Name</span></td>
        <td><span class="d-flex pt-1 pb-1 font-bold">Beneficiary Parent Name</span></td>
    </tr>
    <tr>
        <td><span class="d-flex">{{name}}</span></td>
        <td><span class="d-flex">{{parentName}}</span></td>
    </tr>
```

b. Any modifications that you make (such as combining address fields as a single string) to the address value must be performed in controller.js. The dynamic values will be sent from[ **controller.js**](https://github.com/egovernments/DIVOC/blob/main/backend/certificate\_api/src/routes/certificate\_controller.js)

```
function prepareDataForVaccineCertificateTemplate(certificateRaw, dataURL) {
    certificateRaw.certificate = JSON.parse(certificateRaw.certificate);
    const {certificate: {credentialSubject, evidence}} = certificateRaw;
    const certificateData = {
        name: credentialSubject.name,
        parentName: credentialSubject.parentName,
        age: credentialSubject.age,
        gender: credentialSubject.gender,
        identity: formatId(credentialSubject.id),
        beneficiaryId: credentialSubject.refId,
        recipientAddress: formatRecipientAddress(credentialSubject.address),
        vaccine: evidence[0].vaccine,
        vaccinationDate: formatDate(evidence[0].date) + ` (Batch no. ${evidence[0].batch} )`,
        vaccineValidDays: `after ${getVaccineValidDays(evidence[0].effectiveStart, evidence[0].effectiveUntil)} days`,
        vaccinatedBy: evidence[0].verifier.name,
        vaccinatedAt: formatFacilityAddress(evidence[0]),
        qrCode: dataURL,
        dose: evidence[0].dose,
        totalDoses: evidence[0].totalDoses,
        isFinalDose: evidence[0].dose === evidence[0].totalDoses,
        currentDoseText: `(${getNumberWithOrdinal(evidence[0].dose)} Dose)`
    };

    return certificateData;
}
```

**Note:**&#x20;

* To check the PDF/print version, which will be generated after an update, open the HTML file in the browser and check for the print preview.&#x20;
* The page size should be A4 as the HTML is developed according to A4 dimensions.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
