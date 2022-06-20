# Payload Changes in the QR Code

* DIVOC certificates are natively digital, verifiable, digitally signed, and also printable with a secure and tamper-proof [**QR code**](../../divocs-verifiable-certificate-features/what-information-goes-into-a-qr-code.md)**.**
* The QR [**payload**](../../divocs-verifiable-certificate-features/divocs-native-covid-19-certificate-specification.md) structure is based on the [**W3C verifiable credentials data model**](https://www.w3.org/TR/vc-data-model/). Previously, any changes in the QR payload required changing it in the certificate-signer service and subsequent deployment.
* Previously, any changes in the QR payload required changing it in the certificate-signer service and subsequent deployment.
* With DIVOC 2.0, QR payload changes can now be made by changing it in etcd without any deployments.
* Currently, only the optional fields that already exist can be removed. New fields cannot be added as of now.
* Note: Do not remove the [**mandatory**](../../divocs-verifiable-certificate-features/what-information-goes-into-a-qr-code.md) fields.

### Steps to remove an optional field:

* Go to DDCC\_TEMPLATE and click on the Edit key If you want to remove an optional field.
* Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../.gitbook/assets/Screenshot 2022-06-20 at 8.50.52 AM.png>)



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._    &#x20;
