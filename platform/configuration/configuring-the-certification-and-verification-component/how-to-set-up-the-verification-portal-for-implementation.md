# How to set up the verification portal for implementation

## Overview&#x20;

The document will help an implementer make changes to DIVOC’s verification component in line with any changes made to the certificate. It could include changes in the QR code section of the certificate or the logo, among others.

This section will cover the steps to update the verification component by configuring:&#x20;

1. Verification portal home page&#x20;
2. Verification confirmation page

## Prerequisite: Get details on **on functions used for certificate verification**

1. The user will be directed to the verification page according to the  route defined in [**this**](https://github.com/egovernments/DIVOC/blob/main/public\_app/src/App.js) file:

```
 <div style={{paddingBottom: "3rem", paddingTop: "3rem"}}>
  <Switch>
	<Route exact path={"/"} component={Home}/>
	<Route exact path={config.urlPath + "/login"} component={Login}/>
	<Route exact path={"/side-effects"} component={SideEffects}/>
	<Route exact path={"/feedback"} component={SideEffects}/>
	<PrivateRoute exact path={"/feedback/verify"} component={SubmitSymptomsForm} role={RECIPIENT_ROLE} clientId={RECIPIENT_CLIENT_ID}/>
	<Route exact path={"/dashboard"} component={Dashboard}/>
	<Route exact path={"/verify-certificate"} component={VerifyCertificate}/>
	<Route exact path={"/learn"} component={Learn}/>
	<Route exact path={"/not-found"} component={PageNotFound}/>
 </Switch>
</div>
```

2\. You can configure the timeout period for the camera to read the QR code in **config.CERTIFICATE\_SCAN\_TIMEOUT**.&#x20;

3\. If the camera is unable to read the QR code content, the timeout can be set to retry.

```
const onScanWithQR = () => {
        setShowScanner(true);
        setTimeout(() => {
            if(!result) {
                setShowTimeout(true);
            }
        }, config.CERTIFICATE_SCAN_TIMEOUT);
    };


const onTryAgain = () => {
        setShowTimeout(false);
        setShowScanner(false)
    };
```

4\. The QR code scan is triggered from the ‘VerifyCertificate’ method. Once the QR code is read by the application, it is unzipped using the jsZip library.

## Verification portal home page

#### How to update the verification page:

* The required UI changes, including messaging and branding, can be configured on [**this**](https://github.com/egovernments/DIVOC/blob/main/public\_app/src/components/VerifyCertificate/index.js) **** file.
* You can refer to **** [**this**](https://github.com/egovernments/DIVOC/blob/icmr/verification/src/components/VerifyCertificate/index.js) **** file as an example of a country-specific configuration ([**https://verify.icmr.org.in/**](https://verify.icmr.org.in/)).

## **Verification confirmation page**

#### **How to update the vaccination confirmation details:**

Example: Include the beneficiary’s parent name as a mandatory field in the verification confirmation page.

* Open this file: [**https://github.com/egovernments/DIVOC/blob/main/vaccination-context/vaccination-context.js**](https://github.com/egovernments/DIVOC/blob/main/vaccination-context/vaccination-context.js).
* Add a parameter in the function “vaccinationContextV2” to set the schema.&#x20;

```
"Person": {
      "@id": "schema:Person",
      "@context": {
        "@version": 1.1,
        "@protected": true,
        "refId": "schema:id",
        "uhid": "schema:id",
        "name": "schema:name",
        "age": "schema:Number",
        "gender": "schema:gender",
        "nationality": "schema:nationality",
        "recipientParentName": "schema:name",
        "address": {
          "@id": "schema:PostalAddress",
          "@context": {
            "@version": 1.1,
            "@protected": true,
            "streetAddress": "schema:streetAddress",
            "streetAddress2": "vac:addressLine2",
            "city": "vac:city",
            "district": "vac:district",
            "addressRegion": "schema:addressRegion",
            "postalCode": "schema:postalCode",
            "addressCountry": "schema:addressCountry"
          }
        }
      }
    },
```

* Add recipientParentName in the certificate variable inside the function createCertificate.

```
"certificate": {
    "Name": "Name",
    "Age": "Age",
    "DOB": "DOB",
    "Gender": "Gender",
    "recipientParentName":"Recipient Parent Name",
    "Certificate ID": "Certificate ID",
    "Vaccine Name": "Vaccine Name",
    "Vaccine Type": "Vaccine Type",
    "Date of Issue": "Date of Issue",
    "Valid Until": "Valid Until",
    "Dose": "Dose",
    "Total Doses": "Total Doses",
    "Vaccination Facility": "Vaccination Facility"
  },
```

* Build and deploy your changes.&#x20;
* Click [**here**](../../divocs-verifiable-certificate-features/creating-a-divoc-certificate/what-information-is-included-in-the-divoc-certificate.md) to know what information is included in the DIVOC certificate.

**Note:**

* The ‘recipientParentName’ should match with the key in the QR code Json file available in **** [**main.js**](https://github.com/egovernments/DIVOC/blob/main/backend/certificate\_signer/main.js).
* To remove any value (such as “vaccine type”) from the UI screen, you can remove that parameter in the certification field.

__

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
